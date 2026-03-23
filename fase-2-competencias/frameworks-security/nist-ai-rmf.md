# NIST AI Risk Management Framework (AI RMF)

## O que e

Framework de gestao de risco para sistemas de IA publicado pelo NIST dos EUA. Base regulatoria tecnica internacionalmente relevante.
**URL**: https://airc.nist.gov/RMF | Versao: AI RMF 1.0 (2023)

---

## As 4 Funcoes (GOVERN, MAP, MEASURE, MANAGE)

### GOVERN - Governanca
Estabelecer politicas e responsabilidades para gestao de risco de IA.
**MLSecOps**: Politica de desenvolvimento seguro, aprovacao de modelos, documentacao de processos.
**BR**: CMN 5.274/2025 exige estrutura de governanca de risco equivalente.

### MAP - Mapeamento de Risco
Identificar e categorizar riscos de IA relevantes.
**MLSecOps**: Catalogar modelos em producao com classificacao de risco, threat modeling com ATLAS.
**Na pratica**: O Documento Vivo da Empresa e o instrumento de MAP.

### MEASURE - Medicao
Avaliar riscos com metricas objetivas.
**MLSecOps**: Metricas de robustez adversarial (ART), fairness (SHAP/AIF360), drift (Evidently AI).

### MANAGE - Gestao
Implementar controles e responder a riscos.
**MLSecOps**: Controles SLSA/SBOM/Sigstore, monitoramento continuo, playbooks de incidente, rollback.

---

## Categorias de Risco

| Categoria | Controle MLSecOps |
|---|---|
| Accuracy/Drift | Evidently AI, alertas de performance |
| Explainability | SHAP, LIME, documentacao |
| Fairness | AIF360, testes antes de deploy |
| Privacy | Differential Privacy, data minimization |
| Reliability | SLAs, rollback automatico |
| Security | Controles ATLAS, testes ART |
| Safety | Human-in-the-loop para decisoes criticas |

---

## Mapeamento com Regulacao BR

- **CMN 5.274/2025**: GOVERN (governanca de risco)
- **BCB Resolution 85**: MEASURE + explainability (credit scoring)
- **LGPD Art. 46**: Privacy category (privacidade por design)

---

*Criado: marco 2026 | Repositorio: mlsecops-playbook (privado)*
