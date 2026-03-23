# OWASP Machine Learning Security Top 10

## O que e

Lista dos 10 riscos mais criticos em sistemas de ML. Publicado pela OWASP Foundation.
**URL**: https://owasp.org/www-project-machine-learning-security-top-10

---

## Os 10 Riscos

### ML01 - Input Manipulation (Adversarial Examples)
Manipulacao de entradas para enganar o modelo.
**Controles**: Adversarial training, input validation, confidence thresholds.
**BR financeiro**: Transacoes PIX manipuladas para bypassar antifraude.

### ML02 - Data Poisoning
Injecao de dados maliciosos no dataset de treino.
**Controles**: Validacao estatistica, auditoria de proveniencia, isolamento de fontes.
**BR financeiro**: Fraude infiltrando transacoes forjadas para corromper modelo.

### ML03 - Model Inversion
Extracrao de dados de treino via API de predicao.
**Controles**: Differential Privacy, limitar output da API, rate limiting.
**BR financeiro**: Reconstrucao de dados de clientes do modelo de score (LGPD).

### ML04 - Membership Inference
Determinar se um dado foi usado no treino.
**Controles**: Differential Privacy, regularizacao, nao expor probabilidades.
**BR financeiro**: Identificar dados de clientes especificos no modelo de antifraude.

### ML05 - Model Theft
Roubo da funcionalidade via consultas (modelo replica).
**Controles**: Rate limiting, watermarking, deteccao de padroes anormais de consulta.
**BR financeiro**: Competidor reconstruindo modelo de score de credito.

### ML06 - AI Supply Chain Attacks
Comprometimento de dependencias, modelos pre-treinados ou pipelines.
**Controles**: SBOM, hash verification, Sigstore/Cosign, SLSA Level 2+, pip-audit.
**BR financeiro**: Pacote Python malicioso no pipeline de antifraude.

### ML07 - Transfer Learning Attack
Comprometimento de modelos base usados em fine-tuning.
**Controles**: Verificar procedencia, testes de seguranca antes de fine-tuning.
**BR financeiro**: LLM de model hub comprometido antes de fine-tuning em chatbot bancario.

### ML08 - Model Skewing
Manipulacao via feedback loops ou retreinamento continuo.
**Controles**: Human-in-the-loop, validacao de distribuicao de novos dados, rollback.
**BR financeiro**: Adversarios gerando transacoes para skew o modelo ao longo do tempo.

### ML09 - Output Integrity Attack
Manipulacao dos outputs apos predicao.
**Controles**: Assinatura digital de outputs criticos, MACs, integridade da comunicacao.
**BR financeiro**: Intercept do score de credito entre modelo e sistema de aprovacao.

### ML10 - Model Poisoning
Comprometimento direto do arquivo de modelo (pickle, ONNX).
**Controles**: Hash verification, Sigstore/Cosign, model registry com controle de acesso.
**BR financeiro**: Substituicao do artefato de modelo em producao.

---

## Mapeamento -> ATLAS

| OWASP ML | ATLAS TTP | Prioridade |
|---|---|---|
| ML01 | AML.T0043 Adversarial Examples | CRITICA |
| ML02 | AML.T0020 Data Poisoning | CRITICA |
| ML06 | AML.T0010 Supply Chain | CRITICA |
| ML03 | AML.T0024 Model Inversion | ALTA |
| ML05 | AML.T0016 Model Replication | ALTA |

---

*Criado: marco 2026 | Repositorio: mlsecops-playbook (privado)*
