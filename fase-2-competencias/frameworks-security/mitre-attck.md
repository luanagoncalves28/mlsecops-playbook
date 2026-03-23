# MITRE ATT&CK para MLSecOps

## O que e

MITRE ATT&CK e o framework de referencia para taticas e tecnicas adversarias em sistemas de TI. Complementar ao ATLAS: enquanto ATLAS cobre ataques AO modelo, ATT&CK cobre ataques na INFRA onde o modelo roda.

**URL**: https://attack.mitre.org

---

## Taticas Criticas para Pipeline de ML

### TA0001 - Initial Access
Comprometimento do repositorio Git, notebooks Jupyter expostos, credenciais vazadas.
**Controles**: MFA obrigatorio, notebooks nunca publicos, secrets em Vault/Secret Manager.

### TA0002 - Execution
Execucao de codigo malicioso via dependencias comprometidas no pipeline de treino.
**Controles**: SBOM, ambientes isolados, hash verification de dependencias.

### TA0003 - Persistence
Backdoor em modelo via data poisoning, webhook malicioso no model registry.
**Controles**: Validacao de comportamento em cada retreinamento, monitoramento de integridade.

### TA0005 - Defense Evasion
Ataques adversariais que evitam deteccao, obfuscacao de data poisoning.
**Controles**: Monitoramento multi-camada (input + output + metricas internas).

### TA0006 - Credential Access
Roubo de service accounts com acesso a feature stores, model registries, dados de treino.
**Controles**: Service accounts com menor privilegio, rotacao automatica, auditoria.

### TA0008 - Lateral Movement
Movimento de container comprometido para ambiente de treino ou model registry.
**Controles**: Network segmentation, Kubernetes Network Policies, service mesh com mTLS.

### TA0010 - Exfiltration
Exfiltracao de modelos treinados, datasets, hiperparametros.
**Controles**: DLP em saida, logging de acesso ao model registry, rate limiting.

### TA0040 - Impact
Corrupcao de dados de treino, delecao de modelos, degradacao deliberada de performance.
**Controles**: Backups imutaveis, versionamento com rollback, alarmes de degradacao.

---

## Tecnicas de Alta Prioridade

| Tecnica | ID | Controle Primario |
|---|---|---|
| Phishing para acesso ao pipeline | T1566 | MFA, treinamento |
| Supply Chain de dependencias Python | T1195.001 | SBOM, pip-audit, hash |
| Exfiltracao via HTTPS | T1048.003 | Egress filtering, DLP |
| Container escape | T1611 | Seccomp, AppArmor, privileged=false |
| Credenciais em codigo | T1552.001 | Secret scanning, Vault, OIDC |
| Abuso de service accounts | T1078.004 | IAM least privilege, auditoria |

---

*Criado: marco 2026 | Repositorio: mlsecops-playbook (privado)*
