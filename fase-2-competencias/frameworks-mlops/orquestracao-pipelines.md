# Orquestracao de Pipelines ML

## O que e

Orquestracao de pipelines ML e a automacao e coordenacao das etapas de treinamento, validacao e deploy de modelos de ML de forma reproduzivel, auditavel e segura.

---

## Por que Orquestracao Importa em MLSecOps

- **Reproducibilidade**: Mesmo codigo + mesmos dados = mesmo resultado
- **Auditabilidade**: Cada execucao registrada com rastreabilidade completa
- **Seguranca**: Pipelines automatizados removem intervenco humana ad hoc (menor superficie de ataque)
- **Compliance**: Trilha de auditoria completa para regulacoes (CMN 5.274, BCB 538)
- **Segregacao de funcoes**: Quem treina nao e quem aprova o deploy

---

## Ferramentas de Orquestracao

| Ferramenta | Tipo | Melhor Para | Seguranca |
|------------|------|-------------|----------|
| **Vertex AI Pipelines** | GCP-managed | GCP native, escala | IAM integrado |
| **Apache Airflow** | Open source | Flexibilidade, Python | RBAC, secrets |
| **Kubeflow Pipelines** | K8s-native | Multi-cloud, containers | OIDC, mTLS |
| **Prefect** | Modern, Python | Developer experience | RBAC, secrets |
| **Argo Workflows** | K8s-native | GitOps | RBAC K8s |
| **MLflow Projects** | Lightweight | Experimentos | Token auth |

---

## Pipeline de Treinamento Seguro

```python
# Exemplo: Vertex AI Pipeline com security controls
from kfp.v2 import dsl
from kfp.v2.dsl import component, pipeline

@component(
    base_image='python:3.10-slim',
    packages_to_install=['pandas', 'scikit-learn', 'great-expectations']
)
def validate_data(
    dataset_path: str,
    validation_output: dsl.Output[dsl.Dataset]
):
    """Valida qualidade e integridade dos dados de treinamento"""
    import great_expectations as ge
    # Verifica schema, ranges, nulos, distribuicoes
    # FALHA o pipeline se dados estiverem comprometidos

@component
def train_model(
    dataset: dsl.Input[dsl.Dataset],
    model_output: dsl.Output[dsl.Model],
    experiment_name: str
):
    """Treina modelo com rastreabilidade completa"""
    import mlflow
    mlflow.autolog()  # Registra tudo automaticamente

@component
def security_gate(
    model: dsl.Input[dsl.Model],
    security_report: dsl.Output[dsl.Artifact]
):
    """Testes adversariais e verificacao de seguranca"""
    # ART - Adversarial Robustness Toolbox
    # FALHA se modelo vulneravel a ataques basicos

@component  
def sign_and_register(
    model: dsl.Input[dsl.Model],
    registry_uri: str
):
    """Assina e registra modelo aprovado"""
    # Cosign para assinar
    # MLflow Model Registry para registro

@pipeline(
    name='fraud-detection-training',
    pipeline_root='gs://mlsecops-pipeline-root'
)
def fraud_detection_pipeline(dataset_path: str):
    validate = validate_data(dataset_path=dataset_path)
    
    train = train_model(
        dataset=validate.outputs['validation_output'],
        experiment_name='fraud-v2'
    )
    
    security = security_gate(
        model=train.outputs['model_output']
    )
    security.after(train)  # Apenas apos treinamento
    
    register = sign_and_register(
        model=train.outputs['model_output'],
        registry_uri='vertex://models'
    )
    register.after(security)  # Apenas apos security gate
```

---

## Pipeline de Deploy Seguro (CD para ML)

```yaml
# .github/workflows/ml-deploy.yml
name: ML Model Deploy
on:
  push:
    branches: [main]
    paths: ['models/**']

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: production  # Requer aprovacao manual
    permissions:
      id-token: write
    steps:
      - name: Verify model signature
        run: cosign verify $MODEL_DIGEST
      
      - name: Run integration tests
        run: pytest tests/integration/
      
      - name: Deploy canary (10% traffic)
        run: gcloud ai endpoints deploy-model --traffic-split=10
      
      - name: Wait and monitor (30min)
        run: python scripts/monitor_canary.py --duration=30m
      
      - name: Promote to 100% if healthy
        run: gcloud ai endpoints deploy-model --traffic-split=100
```

---

## Patterns de Seguranca em Pipelines

### Principle of Least Privilege
- Cada step do pipeline tem apenas as permissoes necessarias
- Service account por pipeline, nao compartilhada
- Acesso a datasets apenas durante execucao, nao permanente

### Immutable Artifacts
- Artefatos nunca modificados apos criacao
- Versionamento semantico obrigatorio
- Hash e assinatura para verificacao de integridade

### Segregacao de Ambientes
```
Dev -> Staging -> Pre-prod -> Producao
  Testes unitarios
        Testes de integracao + security gate
                Smoke tests + canary
                            Monitoramento continuo
```

### Secrets Management
- Nunca hardcodar credenciais em pipelines
- HashiCorp Vault ou GCP Secret Manager
- Rotacao automatica de credenciais
- Audit log de acesso a secrets

---

## Checklist de Pipeline Seguro

- [ ] Pipeline 100% automatizado (zero steps manuais fora de aprovacoes)
- [ ] Validacao de dados como step obrigatorio
- [ ] Security gate com testes adversariais
- [ ] Assinatura de artefatos antes do deploy
- [ ] Aprovacao formal requerida antes de producao
- [ ] Rollback automatico configurado
- [ ] Logs de execucao retidos para auditoria
- [ ] Secrets via vault, nunca hardcodados
- [ ] Segregacao de funcoes: treino vs deploy vs aprovacao
