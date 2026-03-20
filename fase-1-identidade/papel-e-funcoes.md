# Papel e Funções do MLSecOps Engineer

---

## O que este arquivo é

Este arquivo define com precisão o papel do MLSecOps Engineer —
o que ele faz, em qual momento faz, o que precisa saber para fazer
bem e como isso se traduz em trabalho reconhecido pelos superiores.

É o mapa de identidade funcional do papel.
Antes de estudar qualquer framework ou ferramenta, entenda isso.

---

## O que o MLSecOps Engineer não é

Antes de definir o que é, é necessário desfazer o entendimento errado
mais comum sobre o papel — porque esse erro compromete a forma como
o profissional age desde o primeiro dia.

**Não é um porteiro do final do pipeline.**
O modelo não chega "pronto" para ele conferir, aprovar e liberar.
Quando o pipeline chega "pronto" para uma conferência final, o problema
já pode ter entrado semanas antes — e com técnicas como force push que
reescrevem histórico Git, nunca seria detectado numa revisão tardia.

**Não é um analista de segurança que analisa relatórios.**
Não fica esperando alertas chegarem. Projeta sistemas para que os
alertas certos existam, monitora ativamente e age antes que o problema
escale.

**Não é um auditor externo.**
Está dentro do time, costurado no processo, presente em cada fase —
não é alguém que chega depois para avaliar o que outros fizeram.

---

## O que o MLSecOps Engineer é

É o profissional que garante que segurança está integrada em cada
etapa do ciclo de vida de um modelo de ML — da concepção ao
monitoramento contínuo em produção.

Em 2026, com adversários usando IA para automatizar ataques, escalar
exploits e gerar variantes de malware em horas, o MLSecOps Engineer
não pode ser reativo. Precisa ser estruturalmente preventivo — e quando
o imprevisto acontece, precisa ter a estrutura mental e os sistemas
para responder com inteligência e precisão.

---

## As 6 Funções Principais

### Função 1 — Segurança do Ciclo de Vida do Modelo

**O que é:**
Proteger o modelo em cada etapa da sua existência — desde os dados
que o alimentam até o comportamento que apresenta em produção.

**O que precisa saber:**
Como data poisoning funciona e como detectar sinais de manipulação
em datasets de treino. Como garantir integridade de artefatos de modelo
(.pkl, .onnx, .pt) com hash e assinatura digital. Como um modelo pode
vazar dados de treino através de suas predições (model inversion).
Como comportamento adversarial em produção se diferencia de degradação
natural. Como estruturar o model registry com controles de acesso e
rastreabilidade completa de quem promoveu qual versão.

**Como o serviço é reconhecido pelos superiores:**
Quando um modelo em produção apresenta comportamento anômalo, o
MLSecOps Engineer já tem o histórico de integridade para responder
em minutos se foi comprometimento ou degradação — e evidência
documentada para apresentar a qualquer stakeholder ou regulador.
Isso é o que transforma um incidente em demonstração de maturidade
em vez de crise.

---

### Função 2 — Segurança de Supply Chain

**O que é:**
Garantir que tudo que entra no pipeline — bibliotecas Python, datasets,
modelos pré-treinados, containers, extensões de IDE, GitHub Actions —
é íntegro e não foi comprometido antes de chegar ao ambiente da empresa.

**O que precisa saber:**
Como ataques de supply chain funcionam e por onde entram (o ataque
GlassWorm/ForceMemo de março 2026 é o caso de referência — tokens
GitHub roubados via extensões de IDE, force push reescrevendo histórico,
malware em setup.py executado automaticamente no pip install).
Como gerar e verificar SBOM (Software Bill of Materials) de código
e de containers. Como assinar artefatos com Sigstore/Cosign.
Como auditar dependências com pip-audit e socket.dev.
Como configurar branch protection para bloquear force push.
Como usar OIDC efêmero no CI/CD para eliminar tokens permanentes.
Como criar e manter política de extensões aprovadas para IDEs.

**Como o serviço é reconhecido pelos superiores:**
Supply chain attacks são invisíveis até causarem dano catastrófico.
Quando o MLSecOps Engineer detecta um pacote comprometido antes de
entrar em produção, ou bloqueia um force push anômalo automaticamente,
o superior raramente vê — porque não houve incidente. A visibilidade
aqui vem de relatórios regulares de postura: "bloqueamos X tentativas,
auditamos Y dependências, zero comprometimentos confirmados no período."
Esse é o serviço que constrói confiança silenciosa e duradoura.

---

### Função 3 — Defesa contra Ameaças e Adversários

**O que é:**
Entender como adversários pensam para antecipar ataques antes que
aconteçam e responder com precisão quando acontecem.

**O que precisa saber:**
MITRE ATLAS — as 15 táticas e 66 técnicas específicas de ataques a
sistemas de ML e IA, incluindo as 14 técnicas novas de 2025 focadas
em AI Agents. MITRE ATT&CK — os TTPs de infraestrutura ao redor do
pipeline. Como conduzir threat modeling de um pipeline ML usando STRIDE
ou PASTA. Como executar red teaming de modelos — testar adversarial
inputs, tentar extração de modelo, tentar inferência de dados de treino.
Como manter inteligência de ameaças atualizada via feeds (StepSecurity,
CISA KEV, OpenSSF, Socket.dev) e integrar novos TTPs ao monitoramento
existente. Como um adversário que usa IA pensa e opera — não apenas
os ataques conhecidos mas a lógica por trás deles.

**Como o serviço é reconhecido pelos superiores:**
Quando o MLSecOps Engineer apresenta um threat model com os vetores
de ataque específicos para aquele tipo de negócio — não uma lista
genérica de riscos, mas um mapa de "como um adversário atacaria
especificamente este modelo, este pipeline, esta empresa" — ele
demonstra o pensamento estratégico que distingue o profissional
de nível sênior. Superiores reconhecem isso porque é raro e
diretamente conectado à proteção do negócio.

---

### Função 4 — Governança, Risco e Conformidade

**O que é:**
Garantir que modelos e pipelines estão em conformidade com a regulação
vigente, com riscos formalmente gerenciados e com evidências auditáveis
para qualquer fiscalização.

**O que precisa saber:**
No ecossistema financeiro brasileiro: CMN 5.274/2025, BCB 538/2025,
IN BCB 587/2025 (auditabilidade de modelos em antifraude), LGPD
(base legal para dados de treino, pseudonimização, RIPD, notificação
à ANPD). Em outros ecossistemas: mapear a regulação equivalente
antes de qualquer outra ação (ANVISA/CFM para healthtech, LGPD
aplicada a dados de consumidor para varejo e foodtech).
Como classificar dados por sensibilidade e definir tratamento correto
para cada categoria. Como documentar decisões de modelo de forma
auditável. Como gerar evidências de controles para auditorias internas
e externas. Como comunicar postura de risco para C-level e board
em linguagem de negócio sem perder precisão técnica.

**Como o serviço é reconhecido pelos superiores:**
Quando o regulador bate à porta — BCB, ANPD, auditoria interna —
e o MLSecOps Engineer consegue apresentar em horas toda a
rastreabilidade de decisões de modelo, evidências de controles
implementados e documentação de conformidade atualizada, o valor
do trabalho se torna inegável. Em ambientes regulados, isso não é
diferencial — é sobrevivência da empresa. Quem entrega isso
consistentemente constrói posição estratégica, não operacional.

---

### Função 5 — Arquitetura e Engenharia de Segurança

**O que é:**
Projetar e implementar os controles técnicos que tornam o ambiente
de ML seguro por construção — não por revisão posterior.

**O que precisa saber:**
Como hardening de CI/CD funciona na prática (GitHub Actions com OIDC,
branch protection, CODEOWNERS, assinatura de commits). Como gerenciar
secrets com Vault, GCP Secret Manager ou AWS Secrets Manager — nunca
em variáveis de ambiente não gerenciadas ou em repositórios.
Como construir containers seguros (imagem base pinada por SHA,
SBOM gerado, Cosign para assinatura, Trivy para scan). Como configurar
Kubernetes com Pod Security Admission e seccomp profiles. Como
implementar egress filtering para que serviços de ML só se comuniquem
com endpoints autorizados. Como aplicar IAM com menor privilégio em
cloud (GCP, AWS, Azure) para cada componente do pipeline. Como usar
SLSA nível 3+ para garantir proveniência de artefatos. Como integrar
ferramentas de detecção (Falco, OPA/Gatekeeper) no ambiente de produção.

**Como o serviço é reconhecido pelos superiores:**
Engenharia de segurança bem feita é invisível — o ambiente simplesmente
funciona sem incidentes. A visibilidade vem de duas formas: quando
um ataque é bloqueado automaticamente pelos controles implementados
(e o relatório mostra o que foi tentado e o que impediu), e quando
um time externo tenta penetrar o ambiente e encontra resistência
estrutural em vez de buracos pontuais. O MLSecOps Engineer que
constrói esse ambiente é reconhecido como fundação do produto, não
como custo de compliance.

---

### Função 6 — Detecção, Resposta e Recuperação

**O que é:**
Monitorar continuamente, detectar anomalias antes que virem incidentes,
responder com precisão quando o incidente acontece e aprender
estruturadamente com cada ocorrência.

**O que precisa saber:**
Como construir monitoramento em três camadas para modelos em produção:
input monitoring (detectar anomalias de distribuição nos dados que
entram), behavior monitoring (detectar degradação súbita ou spikes
que indiquem adversarial inputs), output monitoring (detectar respostas
fora do padrão de política ou sinais de exfiltração).
Como integrar telemetria de pipeline ao SIEM corporativo com alertas
diferenciados por severidade. Como identificar a diferença entre
drift natural de dados e sinal de ataque. Como executar rollback
seguro de modelo comprometido sem interromper o serviço.
Como conduzir post-mortem estruturado que gera aprendizado real.
Como comunicar incidente para stakeholders, C-level e reguladores
com a linguagem e o timing corretos para cada audiência.

**Como o serviço é reconhecido pelos superiores:**
A resposta a incidentes é onde o MLSecOps Engineer mais aparece —
e onde mais pode construir ou destruir reputação. Um incidente
gerenciado com precisão, comunicado com clareza e encerrado com
post-mortem e melhorias documentadas transforma uma crise em
evidência de maturidade operacional. É o momento mais visível do
trabalho — e quando é feito bem, é inesquecível para quem estava
na sala.

---

## O Momento Exato de Entrada em Cada Fase

```
CONCEPÇÃO DO PROJETO
├── Outros: definem problema de negócio, escolhem abordagem ML
└── MLSecOps: threat modeling, requisitos de segurança,
    classificação de dados, definição de controles necessários

DESENVOLVIMENTO
├── Outros: escrevem código, fazem experimentos, treinam modelos
└── MLSecOps: ambiente de dev seguro, CI/CD com controles integrados,
    auditoria contínua de dependências, linhagem de dados

EXPERIMENTAÇÃO E VALIDAÇÃO
├── Outros: avaliam métricas, ajustam modelo, comparam versões
└── MLSecOps: adversarial testing, model inversion testing,
    validação de integridade do artefato gerado

REGISTRO E PROMOÇÃO PARA PRODUÇÃO
├── Outros: registram modelo, solicitam aprovação de deploy
└── MLSecOps: gate formal — valida proveniência, conformidade
    regulatória, assina aprovação com justificativa documentada

PRODUÇÃO E MONITORAMENTO CONTÍNUO
├── Outros: acompanham métricas de negócio e performance
└── MLSecOps: monitoramento adversarial, detecção de anomalias,
    resposta a incidentes, evidências auditáveis, melhoria contínua
```

---

## Como o Papel Varia por Tipo de Business

O papel é o mesmo em qualquer empresa.
O que muda é a velocidade, a formalidade e a profundidade regulatória.

**Banco grande (Itaú, Bradesco, Caixa)**
Gates formais em cada fase com aprovação documentada.
Modelos que afetam crédito ou antifraude têm exigência regulatória
de documentação prévia pelo BCB. O MLSecOps Engineer é consultado
antes mesmo da concepção. Auditoria interna e externa é constante.
Velocidade menor, exigência de rastreabilidade máxima.

**Fintech de crescimento rápido (Nubank, PicPay, Stone)**
Pipeline move mais rápido. O MLSecOps Engineer integra segurança
como código no CI/CD para não virar gargalo. Gates automáticos
substituem aprovação manual em cada commit. Velocidade alta,
controles precisam ser eficientes e invisíveis no fluxo normal.

**Healthtech**
O custo de um modelo comprometido pode ser vida humana — não só
dinheiro ou reputação. O MLSecOps Engineer entra na concepção
para mapear risco clínico de manipulação adversarial.
Regulação de dados de saúde (LGPD para dados sensíveis, CFM, ANVISA)
determina controles específicos desde o design.

**Startup early stage (qualquer setor)**
Frequentemente não tem pipeline estruturado. O MLSecOps Engineer
constrói a fundação segura do zero — não confere algo existente,
projeta como deve ser para que quando crescer já tenha os controles
certos desde a origem. Aqui o impacto de longo prazo é maior
porque o custo de corrigir arquitetura ruim cresce exponencialmente
com o tamanho da empresa do que construir certo desde o início.

---

## O Que o MLSecOps Engineer Precisa Saber Para Ser Reconhecido

Conhecimento técnico sozinho não constrói reconhecimento.
O que constrói é a combinação de quatro dimensões simultâneas:

**Dimensão 1 — Saber técnico profundo**
Dominar as ferramentas, frameworks e controles com profundidade
suficiente para implementar, avaliar e evoluir — não apenas citar.
Saber por que cada controle existe, o que ele protege, onde ele
falha e o que acontece quando não está presente.

**Dimensão 2 — Raciocínio adversarial**
Pensar como o atacante antes de pensar como o defensor.
Para cada sistema, pipeline ou modelo: o que um adversário
buscaria aqui? Por onde entraria? O que exploraria primeiro?
Sem essa dimensão, os controles implementados protegem o que
parece importante — não o que o adversário vai atacar de fato.

**Dimensão 3 — Inteligência de negócio**
Entender o business profundamente o suficiente para saber o que
proteger com prioridade. Num banco, o modelo de antifraude do PIX
é mais crítico que o modelo de recomendação de produtos.
Numa healthtech, o modelo de triagem tem risco de vida que nenhuma
métrica de F1 captura. Sem essa dimensão, o trabalho é tecnicamente
correto e estrategicamente irrelevante.

**Dimensão 4 — Comunicação de valor**
Traduzir o trabalho técnico em linguagem que CEO, CTO, CFO e board
entendem e valorizam. Não "implementamos SLSA nível 3" — mas
"garantimos que nenhum artefato de modelo pode ser substituído
sem rastreabilidade completa, o que elimina o vetor de ataque
que custou US$1,5 bilhão à Bybit em 2025."
Sem essa dimensão, o trabalho excelente permanece invisível
para quem decide promoção, orçamento e estratégia.

---

## O Princípio Central do Papel

O MLSecOps Engineer de excelência em 2026 não é reconhecido
porque resolveu muitos incidentes.

É reconhecido porque os incidentes que poderiam ter acontecido
não aconteceram — e quando acontecem, são resolvidos com uma
precisão que demonstra que o sistema foi construído para isso.

A excelência neste papel é medida pelo que não explode.
E comunicar esse valor de forma que superiores entendam e valorizem
é tão importante quanto o trabalho técnico que o produz.

---

*Criado em: março 2026*
*Repositório: mlsecops-playbook (privado)*
*Localização: fase-1-identidade/papel-e-funcoes.md*
*Atualizar quando o escopo do papel evoluir ou quando novo tipo*
*de business relevante for incorporado ao sistema*

