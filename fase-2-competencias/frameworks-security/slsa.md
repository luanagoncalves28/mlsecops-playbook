# SLSA - Supply-chain Levels for Software Artifacts

## O que e

Framework de seguranca de cadeia de suprimentos de software desenvolvido pelo Google e OpenSSF. Garante integridade de artefatos de software do codigo-fonte ao deploy. URL: https://slsa.dev | Versao: SLSA v1.0 (2023)

---

## Por que SLSA e Critico em MLSecOps

Pipelines de ML tem uma cadeia de suprimentos unica e complexa:
- Datasets de multiplas fontes (potencialmente comprometidas)
- Modelos pre-treinados de repositorios publicos (Hugging Face, etc)
- Bibliotecas de ML com dependencias transitivas
- Artefatos de modelo (pesos, configuracoes) que podem ser adulterados
- Scripts de treinamento que podem ser modificados maliciosamente

---

## Os 4 Niveis SLSA

| Nivel | Requisitos | Protecao |
|-------|------------|----------|
| SLSA 1 | Build automatizado, proveniencia disponivel | Erros acidentais |
| SLSA 2 | Build service, proveniencia autenticada | Adulteracao por mantenedor |
| SLSA 3 | Build hardened, proveniencia nao falsificavel | Comprometimento do build system |
| SLSA 4 (legacy) | Two-party review, build hermetico | Ameacas avancadas |

---

## Aplicacao em Pipelines de ML

### Rastreabilidade de Dados (Data Provenance)
```yaml
# Exemplo: metadados de proveniencia para dataset
subject:
  - name: fraud_dataset_v2.parquet
    digest:
      sha256: abc123def456...
buildType: https://mlops.example.com/data-pipeline
builder:
  id: https://github.com/luanagoncalves28/mlsecops-playbook/.github/workflows/data-pipeline.yml
materials:
  - uri: gs://raw-data-bucket/transactions_2024.csv
    digest:
      sha256: xyz789...
```

### Rastreabilidade de Modelo (Model Provenance)
```yaml
# Proveniencia do modelo treinado
subject:
  - name: fraud_detector_v1.pkl
    digest:
      sha256: model_hash_here
buildType: https://mlops.example.com/training-pipeline
materials:
  - uri: fraud_dataset_v2.parquet  # dataset usado
    digest: {sha256: abc123...}
  - uri: train.py                   # script de treinamento
    digest: {sha256: script_hash...}
  - uri: requirements.txt           # dependencias
    digest: {sha256: deps_hash...}
```

---

## Implementacao Pratica por Nivel

### SLSA Level 1 - Minimo Aceitavel
- [ ] Pipeline de treinamento automatizado (sem steps manuais)
- [ ] Gerar arquivo de proveniencia para cada modelo
- [ ] Versionar datasets com hash SHA-256
- [ ] Usar MLflow ou DVC para rastreabilidade

### SLSA Level 2 - Recomendado para Producao
- [ ] GitHub Actions como build service confiavel
- [ ] Proveniencia assinada com chave do workflow (OIDC)
- [ ] Nenhum humano pode modificar o build apos trigger
- [ ] Artifact registry com verificacao de assinatura

### SLSA Level 3 - Para Sistemas Criticos
- [ ] Build environment efemero e isolado
- [ ] Proveniencia gerada dentro do ambiente isolado
- [ ] Verificacao de dependencias (pip-audit, safety)
- [ ] Registro imutavel de todos os artefatos

---

## Ferramentas do Ecossistema SLSA

| Ferramenta | Funcao | Uso em ML |
|------------|--------|----------|
| **Sigstore/Cosign** | Assinar e verificar artefatos | Assinar modelos e datasets |
| **Rekor** | Log de transparencia imutavel | Registro publico de proveniencia |
| **SLSA GitHub Generator** | Gerar proveniencia automaticamente | Actions para training pipelines |
| **in-toto** | Framework de supply chain policy | Verificar cada step do pipeline |
| **DVC** | Versionamento de dados e modelos | Rastrear datasets e checkpoints |
| **MLflow** | Model registry com metadados | Proveniencia de experimentos |

---

## Integracao com CI/CD para ML

```yaml
# .github/workflows/ml-training.yml
name: ML Training Pipeline
on: [push]
jobs:
  train:
    runs-on: ubuntu-latest
    permissions:
      id-token: write  # necessario para SLSA provenance
      contents: read
    steps:
      - uses: actions/checkout@v4
      - name: Verify dataset integrity
        run: sha256sum -c dataset.sha256
      - name: Train model
        run: python train.py
      - name: Sign model artifact
        uses: sigstore/cosign-installer@v3
      - name: Generate SLSA provenance
        uses: slsa-framework/slsa-github-generator@v1
```

---

## Ameacas Mitigadas por SLSA em ML

| Ameaca | MITRE ATLAS | Mitigacao SLSA |
|--------|-------------|----------------|
| Data Poisoning | AML.T0020 | Proveniencia de dataset + hash verification |
| Model Tampering | AML.T0031 | Assinatura de artefatos de modelo |
| Dependency Confusion | - | Lock files + verificacao de hash |
| Compromised Training Script | AML.T0019 | Code signing + revision control |
| Malicious Pre-trained Model | AML.T0010 | Verificacao de proveniencia |

---

## Mapeamento Regulatorio

- **NIST CSF PROTECT**: Integridade de artefatos como controle de protecao
- **NIST AI RMF MANAGE**: Rastreabilidade como parte de gestao de riscos de IA
- **CMN 5.274/2025**: Auditabilidade de sistemas de IA (proveniencia prove trilha)
- **BCB Resolucao 85**: Explainability inclui saber exatamente qual dataset/modelo esta em prod
