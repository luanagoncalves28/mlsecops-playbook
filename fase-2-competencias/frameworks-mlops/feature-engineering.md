# Feature Engineering para MLSecOps

## O que e

Processo de transformar dados brutos em features (variaveis) que melhoram a performance do modelo de ML. Em MLSecOps, a engenharia de features deve tambem considerar seguranca, privacidade e fairness.

---

## Tipos de Features por Dominio

### Features para Deteccao de Fraude (PIX/Financeiro)

**Comportamentais:**
- Frequencia de transacoes por periodo (hora, dia, semana)
- Valor medio historico por tipo de transacao
- Desvio padrao do valor das transacoes
- Horario tipico de transacoes do usuario
- Numero de destinatarios unicos por periodo

**Baseadas em Grafo:**
- Grau de conectividade na rede de transacoes
- Centralidade do no na rede
- Numero de comunidades a que pertence
- Historico de transacoes com novas contrapartes

**Contextuais:**
- Distancia geografica entre remetente e destinatario
- Dispositivo utilizado (novo vs habitual)
- Hora e dia da semana
- Velocidade de transacoes (muitas em curto periodo)

**Agregadas:**
- Rolling window: media movel 7, 14, 30 dias
- Velocidade de gasto: valor no ultimo 1h vs media 30 dias
- RFM: Recencia, Frequencia, Monetario

---

## Feature Store - Conceito e Implementacao

### O que e Feature Store
Repositorio centralizado para armazenar, documentar e servir features de ML de forma consistente entre treinamento e inferencia.

### Problema resolvido: Training-Serving Skew
```
SEM feature store:
  Treinamento: feature calculada de forma X
  Producao: mesma feature calculada de forma Y (diferente!)
  Resultado: modelo performa mal em producao

COM feature store:
  Treinamento e Producao: mesma logica de calculo, sempre
  Resultado: consistencia garantida
```

### Ferramentas de Feature Store
| Ferramenta | Tipo | Melhor Para |
|------------|------|-------------|
| **Feast** | Open source | Flexibilidade, Kubernetes |
| **Tecton** | Managed | Empresas, SLA garantido |
| **Vertex AI Feature Store** | GCP | Integracao GCP |
| **SageMaker Feature Store** | AWS | Integracao AWS |
| **Databricks Feature Store** | Managed | Ecossistema Databricks |

---

## Perspectiva de Seguranca em Feature Engineering

### 1. Feature Leakage (Vazamento de Dados)
**O que e:** Features que contem informacao do futuro ou do target, causando overfitting irreal.

**Exemplos perigosos:**
- Usar data de fraude confirmada como feature para prever fraude
- Usar saldo pos-transacao para prever se transacao vai ocorrer

**Como prevenir:**
- Analise temporal rigorosa
- Point-in-time correct features
- Auditoria de features pre-treinamento

### 2. Feature Privacy (Privacidade)
**Dados pessoais como features:**
- CPF, email, nome: nunca usar diretamente - tokenizar
- Localizacao: usar em nivel de cidade/regiao, nao preciso
- Dados de saude: base legal rigorosa, minimizacao

**Tecnicas de privacidade:**
- Hashing one-way para identificadores
- Bucketing para idades, salarios
- Generalizacao de dados geograficos
- Differential privacy no calculo de features agregadas

### 3. Feature Poisoning
**Ameaca:** Atacante manipula dados de entrada para influenciar features e enganar o modelo.

**Defesas:**
- Validacao de range e distribuicao de features na inferencia
- Monitoramento de distribuicao de features em producao
- Alertas para features fora dos limites esperados
- Feature importance monitoring

### 4. Bias em Features
**Fontes de bias:**
- Historico discriminatorio nos dados (ex: credito negado historicamente para grupos)
- Features proxy para atributos protegidos (CEP como proxy para raca)
- Sub-representacao de grupos nos dados de treinamento

**Ferramentas de avaliacao:**
- **AIF360** (IBM): Metricas de fairness, remocao de bias
- **Fairlearn** (Microsoft): Reducao de disparidades
- **What-If Tool** (Google): Exploracao visual

---

## Pipeline de Feature Engineering Seguro

```python
# Exemplo: Pipeline de features para deteccao de fraude
import pandas as pd
from great_expectations import DataContext

def create_fraud_features(df: pd.DataFrame) -> pd.DataFrame:
    # 1. Features de velocidade
    df['tx_velocity_1h'] = df.groupby('account_id')['amount'] \
        .transform(lambda x: x.rolling('1H').count())
    
    # 2. Desvio do comportamento historico  
    df['amount_deviation'] = (df['amount'] - df['avg_amount_30d']) / df['std_amount_30d']
    
    # 3. Feature de dispositivo novo
    df['new_device'] = ~df['device_hash'].isin(df['known_devices'])
    
    # SEGURANCA: validar features antes de usar
    validate_features(df)
    
    return df

def validate_features(df: pd.DataFrame):
    # Great Expectations para validacao de qualidade
    assert df['tx_velocity_1h'].between(0, 100).all(), 'Velocity anomala'
    assert not df[['amount_deviation', 'new_device']].isnull().any().any()
```

---

## Checklist de Feature Engineering Seguro

- [ ] Features documentadas com descricao, tipo e fonte
- [ ] Verificacao de feature leakage
- [ ] Dados pessoais tokenizados/anonimizados
- [ ] Validacao de distribuicao antes de treinamento
- [ ] Avaliacao de bias por grupos demograficos
- [ ] Versionamento de features no feature store
- [ ] Consistencia treinamento-producao verificada
- [ ] Monitoramento de distribuicao de features em producao
