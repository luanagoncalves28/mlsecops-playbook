# Ciclo de Vida do Modelo ML

## Visao Geral

O ciclo de vida de um modelo de Machine Learning em producao abrange desde a definicao do problema de negocio ate a aposentadoria do modelo, passando por etapas criticas de desenvolvimento, validacao, deploy e monitoramento.

---

## As 7 Etapas do Ciclo de Vida

### 1. Definicao do Problema (Problem Framing)
**O que fazer:**
- Definir claramente o objetivo de negocio
- Formular como problema de ML (classificacao, regressao, etc)
- Estabelecer metricas de sucesso (business + ML)
- Avaliar viabilidade e riscos

**Perspectiva MLSecOps:**
- Avaliar se o uso de ML e justificado (nao usar ML onde nao e necessario)
- Identificar dados necessarios e verificar disponibilidade/legalidade
- Avaliar riscos regulatorios (LGPD, CMN 5.274)
- Documentar stakeholders e accountability

### 2. Coleta e Curadoria de Dados
**O que fazer:**
- Identificar fontes de dados
- Coletar e integrar dados
- Avaliar qualidade dos dados
- Documentar linhagem de dados

**Perspectiva MLSecOps:**
- Verificar base legal para uso dos dados (LGPD)
- Inspecionar dados por sinais de poisoning ou manipulacao
- Aplicar hash e assinar datasets (SLSA)
- Separar dados de treinamento, validacao e teste com controle de acesso
- Documentar toda a cadeia de custódia dos dados

### 3. Exploracao e Preparacao (EDA + Feature Engineering)
**O que fazer:**
- Analise exploratoria de dados (EDA)
- Tratamento de valores ausentes e outliers
- Engenharia de features
- Selecao de features

**Perspectiva MLSecOps:**
- Anonimizar/pseudonimizar dados sensiveis antes de EDA
- Controle de acesso ao ambiente de experimentacao
- Versionar datasets preparados com DVC
- Testar features para sinais de data leakage
- Avaliar fairness das features (bias potencial)

### 4. Treinamento e Experimentacao
**O que fazer:**
- Selecao de algoritmos
- Treinamento de modelos
- Hyperparameter tuning
- Comparacao de experimentos

**Perspectiva MLSecOps:**
- Ambiente de treinamento isolado e auditado
- Registrar todos os experimentos (MLflow)
- Verificar reproducibilidade (seeds fixos, versoes de bibliotecas)
- Escanear dependencias por vulnerabilidades (pip-audit)
- Avaliar robustez adversarial antes de prosseguir
- Documentar metricas de bias e fairness

### 5. Validacao e Avaliacao
**O que fazer:**
- Avaliar performance no conjunto de teste
- Validar metricas de negocio
- Analise de erros
- Testes de robustez

**Perspectiva MLSecOps:**
- **Security gate**: criterios de seguranca devem ser atendidos antes do deploy
- Testes adversariais (ART - Adversarial Robustness Toolbox)
- Avaliacao de fairness por grupos demograficos (AIF360)
- Teste de membership inference (privacidade de dados de treino)
- Verificacao de explicabilidade (SHAP, LIME)
- Revisao por pares obrigatoria para modelos criticos

### 6. Deploy e Servico
**O que fazer:**
- Empacotamento do modelo
- Configuracao de inferencia
- Deploy em ambiente de producao
- Validacao pos-deploy (smoke tests)

**Perspectiva MLSecOps:**
- Assinar artefato do modelo antes do deploy (Cosign/Sigstore)
- Verificar assinatura no destino antes de servir
- Deploy progressivo: canary -> A/B -> 100%
- Rate limiting e autenticacao no endpoint de inferencia
- Sanitizacao de inputs na API
- Logging de predicoes para auditoria
- Rollback automatico se metricas degradarem

### 7. Monitoramento e Manutencao
**O que fazer:**
- Monitorar performance em producao
- Detectar drift de dados e conceito
- Decidir quando re-treinar
- Aposentar modelo quando necessario

**Perspectiva MLSecOps:**
- Alertas de degradacao de performance
- Deteccao de inputs anomalos (adversarial probe)
- Monitoramento de fairness em tempo real
- Auditoria periodica do modelo
- Processo formal de aposentadoria com limpeza de dados

---

## Gates de Seguranca por Etapa

| Etapa | Gate de Seguranca | Criterio de Aprovacao |
|-------|-------------------|-----------------------|
| Coleta | Verificacao legal | Base legal documentada |
| Preparacao | Auditoria de dados | Sem PII exposto |
| Treinamento | Scan de dependencias | Zero CVEs criticos |
| Validacao | Security assessment | ART score > threshold |
| Deploy | Assinatura e aprovacao | Artefato assinado + aprovacao |
| Producao | Monitoramento ativo | Dashboard operacional |

---

## Ferramentas por Etapa

| Etapa | Ferramentas |
|-------|-------------|
| Coleta/EDA | Pandas, Great Expectations, dbt |
| Versionamento | DVC, MLflow, Git |
| Treinamento | Scikit-learn, XGBoost, PyTorch |
| Seguranca | ART, AIF360, pip-audit, Snyk |
| Experimentos | MLflow Tracking, Weights & Biases |
| Deploy | BentoML, Seldon, KServe, FastAPI |
| Monitoramento | Evidently AI, Arize, Grafana |
| Assinatura | Cosign, Sigstore, in-toto |
