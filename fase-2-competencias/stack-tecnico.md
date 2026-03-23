# Stack Técnico MLSecOps Engineer — 2026

## Como usar este arquivo

Este é o mapa do arsenal técnico completo do Engenheiro MLSecOps. Para cada ferramenta ou tecnologia: o que é, para que serve no contexto MLSecOps, e em qual nível de profundidade é necessário dominar.

Níveis:
- **Usar**: saber usar no dia a dia, configurar, debugar
- **Entender**: saber como funciona, avaliar, escolher entre alternativas
- **Conhecer**: saber o que é, quando usar, onde buscar referência

---

## 1. Linguagens e Ambientes

| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| Python 3.10+ | Usar | Scripts de segurança, pipelines, testes adversariais |
| SQL | Usar | Query em feature stores, audit logs, análise de deriva de dados |
| YAML | Usar | CI/CD configs, Kubernetes manifests, pipeline definitions |
| Bash/Shell | Usar | Automacao de scripts de seguranca, pre-commit hooks |
| Terraform/IaC | Entender | Provisionamento seguro de infraestrutura de ML |
| Go (basico) | Conhecer | Ferramentas de seguranca como Trivy, Cosign são escritas em Go |

---

## 2. ML Engineering Stack

### 2.1 Orquestração de Pipelines
| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| Kubeflow Pipelines | Entender | Pipeline de treino com controles de acesso e auditoria |
| Vertex AI Pipelines (GCP) | Usar | Pipeline MLOps nativo em GCP com IAM integrado |
| Apache Airflow | Entender | Orquestração com auditoria de execução |
| MLflow | Usar | Rastreamento de experimentos, versionamento de modelos |
| DVC | Entender | Versionamento de dados com integridade verificavel |

### 2.2 Serving e Deployment
| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| Docker | Usar | Containers imutaveis, hardening de imagens |
| Kubernetes | Entender | Deploy seguro, RBAC, network policies |
| FastAPI | Usar | APIs de inferencia com autenticacao e rate limiting |
| Seldon Core / KServe | Conhecer | Serving de modelos com controles de acesso |
| BentoML | Conhecer | Empacotamento de modelos com dependencias fixadas |

### 2.3 Feature Stores
| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| Feast | Entender | Feature store open-source com controle de acesso |
| Vertex AI Feature Store | Usar | Feature store gerenciada no GCP |
| Tecton | Conhecer | Feature store enterprise com auditoria avancada |

### 2.4 Monitoramento de Modelos
| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| Evidently AI | Usar | Drift detection, data quality, adversarial monitoring |
| WhyLogs / whylabs | Usar | Logging estatistico para deteccao de anomalias |
| Prometheus + Grafana | Entender | Metricas de infra e modelo em tempo real |
| Vertex AI Model Monitoring | Usar | Monitoramento nativo GCP |

---

## 3. Security Stack

### 3.1 Seguranca de Supply Chain
| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| Sigstore / Cosign | Usar | Assinatura digital de artefatos de modelo e containers |
| SLSA Framework | Usar | Niveis de proveniencia de artefatos (L1-L3) |
| Syft | Usar | Geracao de SBOM (Software Bill of Materials) |
| Grype / Trivy | Usar | Scan de vulnerabilidades em containers e dependencias |
| pip-audit | Usar | Scan de CVEs em dependencias Python |
| Dependabot / Renovate | Entender | Atualizacao automatica de dependencias com CVEs |

### 3.2 Seguranca de CI/CD
| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| GitHub Actions | Usar | Pipelines com OIDC, sem tokens permanentes |
| HashiCorp Vault | Entender | Gestao de segredos com rotacao automatica |
| Google Secret Manager | Usar | Segredos em GCP com auditoria de acesso |
| SAST tools (Bandit, Semgrep) | Usar | Analise estatica de seguranca em codigo Python |
| OPA / Rego | Conhecer | Policy-as-code para aprovacao de modelos |

### 3.3 Cloud Security (GCP Focus)
| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| Google Cloud IAM | Usar | Principio de menor privilegio para pipelines de ML |
| VPC Service Controls | Entender | Perimetro de seguranca para dados sensiveis |
| Cloud Audit Logs | Usar | Auditoria de acesso a dados e modelos |
| BeyondCorp / IAP | Conhecer | Acesso zero-trust a recursos de ML |
| Cloud Armor | Conhecer | Protecao de APIs de inferencia |

### 3.4 Testes Adversariais
| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| Adversarial Robustness Toolbox (ART) | Usar | Testes de adversarial attacks: FGSM, PGD, C&W |
| CleverHans | Entender | Biblioteca de ataques adversariais em TensorFlow/PyTorch |
| Foolbox | Entender | Ataques adversariais agnosè a framework |
| TextAttack | Conhecer | Ataques adversariais em modelos de NLP |

---

## 4. Observabilidade e Resposta a Incidentes

| Tecnologia | Nível | Uso MLSecOps |
|---|---|---|
| ELK Stack (Elasticsearch, Logstash, Kibana) | Entender | Centralizacao e analise de logs de pipeline e modelo |
| OpenTelemetry | Entender | Tracing distribuido de requisicoes de inferencia |
| PagerDuty / OpsGenie | Conhecer | Alertas e escalacao de incidentes |
| SIEM (Splunk, Chronicle) | Conhecer | Correlacao de eventos de seguranca em escala |

---

## 5. Plataformas MLOps

| Plataforma | Nível | Nota |
|---|---|---|
| Google Cloud (Vertex AI, GCS, BigQuery) | Usar | Stack principal |
| Databricks | Entender | Comum em empresas financeiras BR |
| AWS SageMaker | Conhecer | Segundo stack mais comum |
| Azure ML | Conhecer | Terceiro stack mais comum |
| Weights & Biases | Entender | Experimentacao e rastreamento |

---

## 6. Frameworks de ML / Deep Learning

| Framework | Nível | Nota |
|---|---|---|
| scikit-learn | Usar | Modelos classicos, baseline, auditoria de fairness |
| XGBoost / LightGBM | Usar | Dominante em financeiro BR (fraude, credito) |
| PyTorch | Entender | Deep learning, modelos adversariais |
| TensorFlow / Keras | Entender | Deploy com TF Serving |
| HuggingFace Transformers | Entender | LLMs e NLP em producao |
| SHAP / LIME | Usar | Explainability para auditoria regulatoria |

---

## Prioridade de Aprendizado (2026)

Ordem de prioridade para desenvolver profundidade:

1. **Critico agora**: Evidently AI, ART, Sigstore/Cosign, pip-audit, GitHub Actions OIDC
2. **Alto valor**: Kubeflow, Vertex AI completo, HashiCorp Vault
3. **Medio prazo**: Databricks Security, OPA/Rego, SIEM integration
4. **Longo prazo**: Go para ferramentas de seguranca, Tekton, Cloud Native Security

---

*Criado: marco 2026*
*Repositorio: mlsecops-playbook (privado)*
*Atualizar: quando nova tecnologia critica emergir ou stack da empresa mudar*
