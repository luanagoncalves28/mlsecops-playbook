# LGPD Aplicada a Machine Learning

## O que e

Lei Geral de Protecao de Dados Pessoais (Lei 13.709/2018) - regulacao brasileira de privacidade equivalente ao GDPR europeu. Entrou em vigor em setembro/2020 com sancoes desde agosto/2021. URL: https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm

---

## Conceitos Fundamentais

| Conceito | Definicao | Relevancia ML |
|----------|-----------|---------------|
| **Dado Pessoal** | Informacao que identifica ou pode identificar pessoa natural | Features de treino com CPF, email, comportamento |
| **Dado Sensivel** | Origem racial, saude, biometria, orientacao sexual, etc | Modelos de credito, saude, RH |
| **Titular** | Pessoa natural a quem se referem os dados | Usuario cujos dados treinaram o modelo |
| **Controlador** | Quem decide sobre tratamento dos dados | Empresa que usa o modelo |
| **Operador** | Quem trata os dados em nome do controlador | Plataforma MLOps, cloud provider |
| **Tratamento** | Qualquer operacao com dados pessoais | Coleta, treinamento, inferencia, armazenamento |

---

## Bases Legais para Tratamento em ML

| Base Legal | Quando Usar em ML | Exemplo |
|------------|-------------------|---------||
| Consentimento | Personalizacao nao essencial | Recomendacoes, ads |
| Execucao de Contrato | Servico prestado usa dados para funcionar | Score de credito para concessao |
| Obrigacao Legal | Compliance regulatorio exige o dado | KYC, AML em financeiro |
| Interesse Legitimo | Balancear interesse da empresa vs privacidade | Deteccao de fraude |
| Protecao do Credito | Especifico para analise de risco financeiro | Modelos de inadimplencia |

---

## LGPD e o Ciclo de Vida do Modelo ML

### 1. Coleta de Dados
- [ ] Verificar base legal antes de coletar
- [ ] Coletar somente dados necessarios (minimizacao)
- [ ] Documentar finalidade especifica do uso
- [ ] Registrar consentimento quando aplicavel

### 2. Armazenamento e Preparacao
- [ ] Criptografar dados pessoais em repouso
- [ ] Aplicar pseudonimizacao ou anonimizacao quando possivel
- [ ] Controlar acesso por principio do menor privilegio
- [ ] Definir politica de retencao e descarte

### 3. Treinamento
- [ ] Avaliar se o modelo pode ser treinado com dados anonimizados
- [ ] Logs de treinamento nao devem expor dados pessoais brutos
- [ ] Documentar quais dados pessoais foram usados no treinamento
- [ ] Privacidade Diferencial para datasets altamente sensiveis

### 4. Deploy e Inferencia
- [ ] API de predicao nao deve logar dados pessoais desnecessariamente
- [ ] Implementar mecanismo de exclusao de dados (direito ao esquecimento)
- [ ] Garantir que o modelo nao memorize dados de treinamento
- [ ] Transparencia: informar quando decisao automatizada e usada

### 5. Monitoramento
- [ ] Logs de inferencia com dados pessoais devem ser protegidos
- [ ] Tempo de retencao de logs conforme politica de privacidade
- [ ] Auditoria de acesso aos dados pessoais usados pelo modelo

---

## Art. 20 - Decisoes Automatizadas (Critico para ML)

O titular tem direito a:
- **Revisao humana** de decisoes tomadas unicamente por algoritmos
- **Explicacao** sobre criterios e procedimentos usados
- **Contestacao** de decisoes automatizadas

**Implicacoes para MLSecOps:**
- Modelos de credito, contratacao, seguro PRECISAM ser explicaveis
- Implementar fallback para revisao humana
- Documentar features mais importantes (SHAP values)
- Ter processo definido para contestacao de decisoes

---

## Anonimizacao vs Pseudonimizacao em ML

| Tecnica | Definicao LGPD | Aplicacao ML | Risco |
|---------|----------------|--------------|-------|
| **Anonimizacao** | Dados sem possibilidade de re-identificacao | Dataset totalmente desidentificado | Re-identificacao por linkage attack |
| **Pseudonimizacao** | Substituicao por identificador | Hash de CPF, tokenizacao | Reversivel com chave |
| **Privacidade Diferencial** | Ruido matematico para privacidade | Federated learning, DP-SGD | Accuracy trade-off |
| **K-Anonimidade** | Cada registro igual a k-1 outros | Dados demograficos | Attribute disclosure |

---

## Sancoes e Penalidades

- Advertencia com prazo para correcao
- Multa simples: ate 2% do faturamento, maximo R$ 50 milhoes por infracao
- Multa diaria
- Publicizacao da infracao
- Bloqueio ou eliminacao dos dados
- Suspensao parcial ou total da atividade de tratamento

**Autoridade Nacional de Protecao de Dados (ANPD)**: orgao regulador

---

## Mapeamento com Outros Frameworks

- **NIST AI RMF - GOVERN**: Politicas de privacidade como governanca de IA
- **NIST CSF - PROTECT**: Controles tecnicos de protecao de dados pessoais
- **OWASP ML Top 10 - ML05**: Membership inference ataca privacidade de dados de treino
- **CIS Control 3**: Protecao de dados pessoais como controle prioritario
- **BCB Resolucao 85**: Explainability de credito alinhada ao Art. 20 LGPD
