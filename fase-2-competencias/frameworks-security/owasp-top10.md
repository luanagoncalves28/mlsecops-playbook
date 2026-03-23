# OWASP Top 10 para MLSecOps

## O que e

OWASP Top 10 lista os riscos mais criticos em aplicacoes web. Para MLSecOps, relevante para proteger APIs de inferencia e interfaces administrativas.
**URL**: https://owasp.org/www-project-top-ten

---

## Riscos com Foco em ML

### A01 - Broken Access Control
**Em ML**: Acesso nao autorizado ao model registry, endpoints de treino, feature store.
**Controles**: RBAC rigoroso, principio de menor privilegio, auditoria de acesso.

### A02 - Cryptographic Failures
**Em ML**: Dados de treino sem criptografia, modelos sem protecao em repouso.
**Controles**: TLS 1.3, criptografia em repouso para dados e modelos.

### A03 - Injection
**Em ML**: SQL injection em queries de features, prompt injection em LLMs.
**Controles**: Parametrizacao de queries, validacao de input, sandboxing para LLMs.

### A04 - Insecure Design
**Em ML**: Pipeline sem gates de seguranca, modelo em prod sem monitoramento.
**Controles**: Threat modeling no design, security by design desde a concepcao.

### A05 - Security Misconfiguration
**Em ML**: Jupyter sem autenticacao, APIs sem rate limiting, buckets GCS/S3 publicos com dados.
**Controles**: Hardening de configuracoes, scans periodicos de misconfiguration.

### A06 - Vulnerable and Outdated Components
**Em ML**: TensorFlow/PyTorch/scikit-learn com CVEs, bibliotecas desatualizadas.
**Controles**: pip-audit, Dependabot, SBOM, politica de atualizacao.

### A07 - Authentication Failures
**Em ML**: Service accounts sem MFA, tokens permanentes em CI/CD.
**Controles**: MFA obrigatorio, OIDC para CI/CD, rotacao automatica de credenciais.

### A08 - Software and Data Integrity Failures
**Em ML**: Artefatos de modelo sem assinatura, pipelines sem verificacao de hash.
**Controles**: Sigstore/Cosign, SLSA, hash verification em cada deploy.

### A09 - Security Logging and Monitoring Failures
**Em ML**: APIs sem logging, model registry sem auditoria.
**Controles**: Logging de predicoes criticas, auditoria de acesso a dados e modelos.

### A10 - SSRF
**Em ML**: APIs que carregam modelos/datasets de URLs externas exploradas via SSRF.
**Controles**: Whitelist de URLs, validacao de destino antes de buscar recursos externos.

---

## Prioridade para APIs de Inferencia

| Risco | Prioridade |
|---|---|
| A05 Misconfiguration | CRITICA |
| A01 Broken Access Control | CRITICA |
| A06 Outdated Components | ALTA |
| A08 Integrity Failures | ALTA |
| A09 Logging Failures | ALTA |

---

*Criado: marco 2026 | Repositorio: mlsecops-playbook (privado)*
