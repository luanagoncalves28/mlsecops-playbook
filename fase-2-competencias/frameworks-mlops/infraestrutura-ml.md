# Infraestrutura ML

## Visao Geral

Infraestrutura de Machine Learning abrange todos os recursos computacionais, de armazenamento e rede necessarios para treinar, servir e monitorar modelos em producao de forma segura e escalavel.

---

## Componentes da Infraestrutura ML

### 1. Computacao para Treinamento
| Recurso | Uso | Consideracoes de Seguranca |
|---------|-----|----------------------------|
| CPUs | Modelos classicos, pre-processamento | IAM, VPC isolation |
| GPUs | Deep learning, embeddings | Custo + acesso controlado |
| TPUs (GCP) | Large models, transformers | Apenas GCP, IAM obrigatorio |
| Spot/Preemptible | Reducao de custo | Nao usar para jobs criticos |

### 2. Armazenamento
| Tipo | Ferramenta | Uso ML | Seguranca |
|------|------------|--------|----------|
| Object Storage | GCS, S3 | Datasets, modelos | Criptografia, ACL, versioning |
| Feature Store | Feast, Tecton | Features calculadas | Acesso por role |
| Model Registry | MLflow, Vertex AI | Artefatos de modelo | Assinatura, imutabilidade |
| Database | BigQuery, Redshift | Labels, metadados | Row-level security |

### 3. Serving (Inferencia)
| Opcao | Latencia | Throughput | Seguranca |
|-------|---------|-----------|----------|
| REST API (FastAPI) | Baixa | Medio | Auth, rate limiting |
| gRPC | Muito baixa | Alto | mTLS |
| Batch prediction | N/A | Muito alto | IAM, encryption |
| Streaming (Kafka+ML) | Media | Alto | SSL, SASL auth |

---

## Arquitetura de Referencia: MLSecOps no GCP

```
[Fontes de Dados]
  BigQuery (transacoes) -> Vertex AI Pipelines
                                    |
                          [Feature Engineering]
                          Dataflow + Feature Store
                                    |
                          [Treinamento Seguro]
                          Vertex AI Training
                          - VPC Service Controls
                          - Customer-managed encryption
                          - Workload Identity
                                    |
                          [Registro e Validacao]
                          Vertex AI Model Registry
                          - Assinatura com Cosign
                          - Security scan
                                    |
                          [Deploy Controlado]
                          Vertex AI Endpoints
                          - Canary deployment
                          - Traffic splitting
                                    |
                          [Monitoramento]
                          Vertex AI Model Monitoring
                          + Cloud Monitoring
                          + Evidently AI
```

---

## Seguranca da Infraestrutura ML

### Principios de Seguranca

**Zero Trust para ML:**
- Nenhum componente e confiavel por default
- Autenticacao e autorizacao em cada comunicacao
- Service accounts dedicadas por servico
- Workload Identity ao inves de chaves

**Isolamento de Rede:**
- VPC dedicada para workloads de ML
- Private Google Access para servicos GCP
- VPC Service Controls para impedir exfiltracao
- Firewall rules restritivas

**Criptografia:**
- Dados em repouso: AES-256 (CMEK para dados sensiveis)
- Dados em transito: TLS 1.2+
- Chaves gerenciadas pelo cliente (CMEK)
- Rotacao periodica de chaves

### Infrastructure as Code (IaC)
```hcl
# terraform/ml-infrastructure/main.tf
resource "google_vertex_ai_endpoint" "fraud_detector" {
  name         = "fraud-detection-endpoint"
  display_name = "Fraud Detection Model"
  location     = "us-central1"
  
  encryption_spec {
    kms_key_name = var.kms_key_name  # CMEK
  }
  
  network = "projects/${var.project}/global/networks/${var.vpc_name}"
}

resource "google_storage_bucket" "ml_artifacts" {
  name          = "mlsecops-artifacts-${var.project}"
  location      = "US"
  force_destroy = false
  
  versioning {
    enabled = true  # Imutabilidade de artefatos
  }
  
  encryption {
    default_kms_key_name = var.kms_key_name
  }
}
```

---

## Gestao de Custos e Capacidade

| Componente | Estrategia de Custo | Risco de Seguranca |
|------------|---------------------|--------------------|
| Treinamento | Spot instances, budget alerts | Nao usar spot para jobs criticos |
| Serving | Auto-scaling, min replicas=1 | DDoS pode escalar custos |
| Storage | Lifecycle policies, nearline | Nao deletar dados com retencao legal |
| Monitoramento | Sampling de logs | Nao amostrar logs de seguranca |

---

## Checklist de Infraestrutura Segura

- [ ] Toda infraestrutura definida como IaC (Terraform)
- [ ] VPC dedicada para workloads de ML
- [ ] Service accounts com least privilege
- [ ] CMEK habilitado para dados sensiveis
- [ ] VPC Service Controls configurados
- [ ] Budget alerts configurados
- [ ] Backup e disaster recovery testados
- [ ] Security Command Center habilitado (GCP)
