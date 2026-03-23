# MITRE ATLAS — Adversarial Threat Landscape for AI Systems

## O que e

MITRE ATLAS e o framework de referencia para taticas, tecnicas e procedimentos (TTPs) de ataques a sistemas de Machine Learning e IA. Mantido pela MITRE Corporation.

**URL**: https://atlas.mitre.org

---

## Por que e central para MLSecOps

ATLAS e o unico framework que mapeia ameacas especificas ao modelo de ML. Enquanto ATT&CK cobre infra, ATLAS cobre o modelo: como e atacado, manipulado, extraido e envenenado.

---

## As 14 Taticas do ATLAS

| Tatica | ID | O que significa |
|---|---|---|
| Reconnaissance | AML.TA0002 | Adversario mapeia sistema de ML, endpoints, datasets expostos |
| Resource Development | AML.TA0000 | Prepara infraestrutura, modelos sombra para ataques |
| ML Attack Staging | AML.TA0001 | Preparacao para atacar o modelo: exemplos adversariais |
| Initial Access | AML.TA0004 | Como o adversario entra: API publica, supply chain, insider |
| Execution | AML.TA0002 | Execucao de codigo malicioso no ambiente de ML |
| Persistence | AML.TA0005 | Manutencao de acesso apos comprometimento inicial |
| Privilege Escalation | AML.TA0006 | Escalamento para acessar dados de treino, modelos privilegiados |
| Defense Evasion | AML.TA0007 | Como o adversario evita deteccao |
| Credential Access | AML.TA0008 | Roubo de credenciais para acessar pipelines de ML |
| Discovery | AML.TA0009 | Mapeamento interno: quais modelos existem, quais dados |
| Collection | AML.TA0010 | Coleta de dados de treino, features, modelos |
| ML Model Access | AML.TA0011 | Acesso via API black-box ou acesso direto white-box |
| Exfiltration | AML.TA0012 | Exfiltracao de dados de treino, arquitetura, hiperparametros |
| Impact | AML.TA0013 | Manipulacao de predicoes, degradacao, negacao de servico |

---

## Tecnicas Criticas para Financeiro BR

### AML.T0020 - Data Poisoning
Injecao de dados maliciosos no dataset de treino.
**No financeiro BR**: Fraude pode infiltrar transacoes forjadas para treinar o modelo a aprovar padroes de fraude.
**Controles**: Validacao estatistica de distribuicao, auditoria de proveniencia, isolamento de fontes.

### AML.T0043 - Adversarial Examples
Entradas manipuladas para enganar o modelo.
**No financeiro BR**: Transacoes PIX com features modificadas para passar pelo modelo de antifraude.
**Controles**: Adversarial training, input distribution monitoring, limites de confianca.

### AML.T0024 - Model Inversion
Uso da API para reconstruir dados de treino.
**No financeiro BR**: Exfiltracao de dados de clientes do modelo de score de credito (LGPD).
**Controles**: Differential Privacy, limitar output da API, rate limiting, auditoria de consultas.

### AML.T0046 - Membership Inference
Determinar se um registro foi usado no treino.
**No financeiro BR**: Violacao de privacidade identificando clientes no modelo de antifraude.
**Controles**: Differential Privacy, regularizacao para reduzir overfitting.

### AML.T0010 - ML Supply Chain Compromise
Comprometimento de dependencias ou pipelines.
**No financeiro BR**: Pacote Python malicioso na cadeia de dependencias do pipeline de antifraude.
**Controles**: SBOM, pin de versoes + hash, Sigstore/Cosign, SLSA Level 2+.

---

## Mapeamento ATLAS por Fase do Pipeline

| Fase | TTPs Relevantes | Controles Primarios |
|---|---|---|
| Coleta de Dados | Data Poisoning | Validacao de fonte, auditoria de proveniencia |
| Feature Engineering | Feature Manipulation | Feature store com controle de acesso |
| Treino | Model Poisoning, Backdoor | Validacao de dataset, ambientes isolados |
| Validacao | Evasion, Model Stealing | Testes adversariais automatizados |
| Deployment | Supply Chain, Artifact Substitution | SLSA, Sigstore, hash verification |
| Inferencia | Adversarial, Inversion, Membership | Rate limiting, input monitoring, DP |
| Monitoramento | Defense Evasion | Anomaly detection, distribuicao de input |

---

*Criado: marco 2026 | Repositorio: mlsecops-playbook (privado)*
