# Papel e Funções do MLSecOps Engineer

---

## O que é este arquivo

Este arquivo define com precisão o papel do MLSecOps Engineer —
o que ele faz, em qual momento faz, o que precisa saber para fazer
bem e como isso se traduz em trabalho reconhecido pelos superiores.

É o mapa de identidade funcional do papel.
Antes de estudar qualquer framework ou ferramenta, entenda isso.

---

## O que o MLSecOps Engineer não é

Antes de definir o que é, é necessário desfazer os entendimentos
errados mais comuns sobre o papel.

**Não é um porteiro do final do pipeline.**
O modelo não chega pronto para ele conferir, aprovar e liberar.
Quando o pipeline chega pronto para uma conferência final,
o problema já pode ter entrado semanas antes.

**Não é só um analista de segurança que analisa relatórios.**
Não fica esperando alertas chegarem. Projeta sistemas para que
os alertas certos existam, monitora ativamente e age antes
que o problema escale.

**Não é um auditor externo.**
Está dentro do time, costurado no processo, presente em cada
fase — não é alguém que chega depois para avaliar o que outros
fizeram.

**Não é só um ML Engineer que aprendeu segurança.**
Nem só um Security Engineer que aprendeu ML. É um profissional
que domina os dois lados com profundidade igual — e entende
como eles se afetam mutuamente em cada decisão de arquitetura,
operação e resposta a incidentes.

---

## O que o MLSecOps Engineer é

É o profissional que garante que pipelines de ML são construídos,
operados e protegidos com excelência — da concepção ao monitoramento
contínuo em produção.

Em 2026, com adversários usando IA para automatizar ataques e
escalar exploits em horas, e com negócios dependendo cada vez mais
de modelos de ML para decisões críticas, o MLSecOps Engineer
não pode ser nem reativo em segurança nem passivo em operações.
Precisa ser estruturalmente preventivo nos dois lados — e quando
o imprevisto acontece, precisa ter a estrutura mental e os sistemas
para responder com inteligência e precisão.

---

## As 10 Funções Principais

O papel tem duas metades que operam juntas e se reforçam
mutuamente. Separar as duas é um erro conceitual — um pipeline
inseguro é um pipeline mal operado, e um pipeline mal operado
cria vulnerabilidades que segurança sozinha não consegue cobrir.

---

### METADE 1 — ML Engineering e Operações

---

### Função 1 — Engenharia e Operação de Pipelines de ML

**O que é:**
Projetar, construir e manter pipelines de ML que funcionam
em produção com confiabilidade, reprodutibilidade e escala.
Não é só fazer o modelo funcionar uma vez — é garantir que
ele funciona consistentemente, pode ser reproduzido, auditado
e evoluído sem quebrar o que já está em produção.

**O que precisa saber:**
Como orquestrar pipelines de treino e inferência com Kubeflow,
Vertex AI Pipelines, Apache Airflow ou Prefect — escolhendo
a ferramenta certa para o contexto e o tamanho do negócio.
Como garantir reprodutibilidade: mesmo código, mesmos dados,
mesmo ambiente deve produzir o mesmo modelo — sempre.
Como versionar não só código mas modelos e dados com DVC,
MLflow ou ferramentas equivalentes.
Como estruturar CI/CD específico para ML — diferente de CI/CD
de software comum porque inclui treino, avaliação e registro
de modelo como etapas do pipeline.
Como fazer o modelo ir de experimento em notebook para
serviço em produção sem perder rastreabilidade nem
introduzir riscos que não existiam no experimento.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: quando o modelo de score de crédito
de uma fintech precisa ser retreinado às 2h porque detectou
que a distribuição de inadimplência do portfólio mudou
significativamente em 48h — evento real que aconteceu com
fintechs brasileiras em 2025 após mudanças no Cadastro Positivo
— o pipeline automatizado faz isso sem intervenção humana,
com rastreabilidade completa e o modelo novo está em produção
antes da abertura do mercado. O superior vê confiabilidade
onde antes via fragilidade.

Contexto universal: empresas de e-commerce em 2026 com modelos
de recomendação enfrentam o problema de concept drift acelerado
— o comportamento do consumidor muda mais rápido do que os
ciclos tradicionais de retreino. Quem tem pipeline automatizado
responde em horas. Quem não tem descobre o problema quando
a receita já caiu.

---

### Função 2 — Gestão de Dados e Feature Engineering

**O que é:**
Garantir que os dados que alimentam os modelos são confiáveis,
rastreáveis, versionados e tratados com o rigor que decisões
críticas de negócio exigem. Features ruins produzem modelos
ruins independente de qual algoritmo você usa.

**O que precisa saber:**
Como projetar e operar uma feature store (Feast, Tecton,
Vertex Feature Store) — onde features são calculadas uma vez,
versionadas e reutilizadas por múltiplos modelos sem duplicação
e sem inconsistência entre treino e produção.
Como garantir linhagem de dados completa: de onde vêm os dados,
quais transformações sofreram, quem teve acesso, qual versão
foi usada para treinar qual modelo.
Como detectar e tratar data quality issues antes que cheguem
ao modelo: valores faltantes, outliers, distribuições anômalas,
data leakage (vazamento de informação do futuro para o passado
no treino).
Como versionar datasets de forma que experimentos sejam
reprodutíveis meses depois.
Como classificar dados por sensibilidade e aplicar
pseudonimização ou anonimização onde a regulação exige.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: em março 2025, o Banco Central identificou
inconsistências em modelos de antifraude de IFs que usavam
dados de PIX sem linhagem documentada — não conseguiam provar
quais dados geraram quais decisões, o que viola diretamente
a IN BCB 587/2025. Quando o regulador pede rastreabilidade
completa de quais dados geraram qual decisão de bloqueio de
transação, você entrega em horas — não em dias de investigação
manual. Isso é o que separa conformidade real de conformidade
de papel.

Contexto universal: healthtechs em 2026 usando modelos de
triagem descobriram que features calculadas de forma diferente
entre treino e produção (training-serving skew) estavam
gerando scores incorretos para pacientes — um problema de
feature store mal implementada que passou despercebido por
meses porque não havia linhagem documentada.

---

### Função 3 — Monitoramento e Observabilidade de Modelos

**O que é:**
Garantir que você sabe o que está acontecendo com o modelo
em produção — não só se ele está respondendo, mas se está
respondendo corretamente, com os dados certos, para os casos
certos. Modelos degradam silenciosamente. Sem monitoramento
adequado, você descobre o problema quando o negócio já foi
impactado.

**O que precisa saber:**
Como implementar monitoramento em três camadas:
— Input monitoring: os dados que chegam ainda têm a mesma
distribuição dos dados de treino? Desvio aqui é o primeiro
sinal de drift ou de ataque adversarial.
— Model monitoring: as predições ainda fazem sentido?
Distribuição de outputs, latência, taxa de confiança.
— Business monitoring: as métricas de negócio que o modelo
influencia estão se comportando como esperado?
Como diferenciar data drift de concept drift — e como
responder a cada um de forma diferente.
Como usar ferramentas de observabilidade: Evidently, WhyLogs,
Arize, Fiddler.
Como definir thresholds de alerta sensíveis sem gerar ruído
que treina os times a ignorar alertas.
Como estruturar o ciclo de retreino: quando retreinar, com
quais dados, como validar antes de promover para produção.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: em 2026, modelos de detecção de fraude
em PIX estão sendo atacados por grupos organizados que testam
pequenas transações para identificar os limites de detecção
do modelo antes de executar o ataque principal — técnica
conhecida como model probing. Input monitoring bem configurado
detecta esse padrão de teste antes do ataque real acontecer.
Quando o CISO pergunta "nosso modelo está sendo sondado?",
você tem a resposta com evidência — não uma estimativa.

Contexto universal: empresas de crédito ao consumidor em 2026
estão enfrentando concept drift acelerado por mudanças no
comportamento de pagamento pós-pandemia que ainda não se
estabilizaram completamente. Modelos treinados com dados de
2023 têm performance degradada em perfis novos de tomadores.
Monitoramento de business metrics — taxa de inadimplência
real vs. prevista pelo modelo — é o que detecta esse desvio
antes que o portfólio de crédito seja materialmente impactado.

---

### Função 4 — Infraestrutura e Plataforma de ML

**O que é:**
Garantir que a infraestrutura que roda os modelos é confiável,
escalável, custo-eficiente e gerenciada como código — não como
conjunto de configurações manuais que só uma pessoa sabe
reproduzir.

**O que precisa saber:**
Como provisionar e gerenciar infraestrutura de ML em cloud
(GCP, AWS, Azure) usando Infrastructure as Code — Terraform
ou equivalente. Nada de configuração manual que não pode
ser versionada.
Como containerizar modelos para inferência com Docker —
imagem base pinada, dependências reprodutíveis, tamanho
otimizado.
Como operar modelos em Kubernetes: deployments, autoscaling,
resource limits, health checks.
Como otimizar custo de inferência: escolha de instância,
batching de requests, caching de predições.
Como fazer model serving eficiente com TorchServe, TF Serving,
BentoML, Ray Serve ou Vertex AI Prediction.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: fintechs brasileiras que operam com
modelos de aprovação de crédito em tempo real enfrentam
picos de request durante datas específicas — abertura do
mercado, pagamento de salários no 5º dia útil, Black Friday
financeiro com antecipação de FGTS. Em novembro 2025,
uma fintech média brasileira registrou pico de 340% acima
da média em requests de crédito pessoal. Pipeline sem
autoscaling bem configurado resulta em timeout de aprovações
— clientes abandonam e vão para o concorrente. Quando o CTO
pergunta quanto custa rodar os modelos em produção e qual
a disponibilidade no último trimestre, você tem a resposta
por modelo, por ambiente, por mês, com SLA documentado.

Contexto universal: empresas de logística em 2026 com modelos
de roteirização dinâmica enfrentam o problema de latência —
o modelo precisa responder em menos de 200ms para não degradar
a experiência do entregador. Infraestrutura mal dimensionada
ou mal configurada não atinge esse SLA em picos de demanda.
O custo de um modelo tecnicamente excelente que não performa
em produção é zero — porque ele não está sendo usado.

---

### METADE 2 — Security

---

### Função 5 — Segurança do Ciclo de Vida do Modelo

**O que é:**
Proteger o modelo em cada etapa da sua existência — desde os
dados que o alimentam até o comportamento que apresenta em
produção.

**O que precisa saber:**
Como data poisoning funciona e como detectar sinais de
manipulação em datasets de treino.
Como garantir integridade de artefatos de modelo (.pkl, .onnx,
.pt) com hash e assinatura digital.
Como um modelo pode vazar dados de treino através de suas
predições (model inversion attack).
Como comportamento adversarial em produção se diferencia
de degradação natural.
Como estruturar o model registry com controles de acesso
e rastreabilidade completa de quem promoveu qual versão.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: em 2025, pesquisadores demonstraram que
modelos de score de crédito treinados com dados de comportamento
bancário eram vulneráveis a model inversion — era possível
inferir faixas de renda e histórico de pagamento de clientes
a partir das predições do modelo. Para um banco que usa esses
dados como segredo estratégico e tem obrigação de proteção
pela LGPD, isso é um incidente de privacidade e de vantagem
competitiva ao mesmo tempo. Quando o DPO pergunta "nosso modelo
pode vazar dados de clientes?", você tem a resposta com
evidência de teste — não uma suposição.

Contexto universal: modelos de LLM fine-tuned em 2026 com
dados corporativos são particularmente vulneráveis a model
inversion e a prompt injection que extrai dados de treino.
Empresas que fine-tunaram modelos com documentos internos
confidenciais descobriram que esses dados podiam ser extraídos
com técnicas específicas de prompting.

---

### Função 6 — Segurança de Supply Chain

**O que é:**
Garantir que tudo que entra no pipeline — bibliotecas Python,
datasets, modelos pré-treinados, containers, extensões de IDE,
GitHub Actions — é íntegro e não foi comprometido antes de
chegar ao ambiente da empresa.

**O que precisa saber:**
Como ataques de supply chain funcionam e por onde entram.
O caso de referência atual é o ataque GlassWorm/ForceMemo
de março 2026: tokens GitHub roubados via extensões maliciosas
de VS Code/Cursor, force push reescrevendo histórico Git sem
rastro, malware em Base64 inserido em setup.py executado
automaticamente no pip install, C2 via campo memo de transações
na blockchain Solana — execução inteiramente em memória
sem gravar em disco.
Como gerar e verificar SBOM de código e de containers.
Como assinar artefatos com Sigstore/Cosign.
Como auditar dependências com pip-audit e socket.dev.
Como configurar branch protection para bloquear force push.
Como usar OIDC efêmero no CI/CD para eliminar tokens
permanentes.
Como criar e manter política de extensões aprovadas para IDEs.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: fintechs brasileiras que usam bibliotecas
Python para processamento de dados de PIX, open finance e antifraude são alvos diretos do vetor
GlassWorm — um desenvolvedor instala uma extensão comprometida,
o token GitHub é roubado, e o próximo pip install de qualquer
membro do time puxa o pacote infectado. Em março 2026, mais de
240 repositórios Python foram comprometidos por essa campanha,
incluindo projetos de ML e pipelines de dados. Quando o CISO
de uma fintech pergunta "temos garantia de que nossas dependências
não foram comprometidas?", você apresenta o relatório de auditoria
contínua de dependências, o histórico de SBOM assinados e o
egress log do CI/CD mostrando zero chamadas anômalas. Isso é
o que transforma supply chain security de controle abstrato
em evidência concreta.

Contexto universal: em 2026, o npm ecosystem registrou mais
de 800 pacotes maliciosos publicados no primeiro trimestre —
número 3x maior que o mesmo período de 2024. Times de ML
que usam pacotes JavaScript para serving de modelos ou
dashboards de monitoramento estão expostos ao mesmo vetor.
A visibilidade vem de relatórios regulares de postura que
mostram o que foi bloqueado antes de chegar em produção.

---

### Função 7 — Defesa Contra Ameaças e Adversários

**O que é:**
Entender como adversários pensam para antecipar ataques antes
que aconteçam e responder com precisão quando acontecem.
Não é conhecer cada ataque específico — é ter a estrutura
de raciocínio que funciona para qualquer ataque, incluindo
os que ainda não existem.

**O que precisa saber:**
MITRE ATLAS — as 15 táticas e 66 técnicas específicas de
ataques a sistemas de ML e IA, incluindo as 14 técnicas novas
de 2025 focadas em AI Agents: prompt injection, memory
poisoning, tool misuse em pipelines de agentes autônomos.
MITRE ATT&CK — os TTPs de infraestrutura ao redor do pipeline:
comprometimento de repositório, roubo de credenciais,
execução via scripts de instalação.
Como conduzir threat modeling de um pipeline ML usando STRIDE
ou PASTA — não como exercício teórico, mas como mapa real
dos vetores de ataque para aquele sistema específico.
Como executar red teaming de modelos: testar adversarial inputs,
tentar extração de modelo, tentar inferência de dados de treino.
Como manter inteligência de ameaças atualizada via feeds
(StepSecurity, CISA KEV, OpenSSF, Socket.dev) e integrar
novos TTPs ao monitoramento existente sem esperar que o
próximo incidente aconteça para atualizar as defesas.
Como um adversário que usa IA pensa e opera em 2026 —
não apenas os ataques conhecidos, mas a lógica por trás:
IA usada para reconhecimento automatizado de repositórios
expostos, geração de variantes de malware que passam por
scanners, engenharia social personalizada baseada em dados
públicos do LinkedIn.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: grupos de fraude organizados no Brasil
em 2026 estão usando modelos de ML próprios para identificar
padrões de detecção dos bancos — eles testam variações de
transações fraudulentas até encontrar o threshold abaixo
do qual o modelo não detecta, depois escalam o ataque.
Isso é adversarial ML aplicado a fraude financeira em tempo
real. Quando você apresenta ao CISO um threat model que
documenta especificamente esse vetor para o modelo de
antifraude do PIX da empresa — com as técnicas MITRE ATLAS
mapeadas, os sinais de detecção definidos e os controles
recomendados — você demonstra que entende o adversário
específico daquele negócio, não um adversário genérico
de livro texto.

Contexto universal: empresas de saúde em 2026 com modelos
de diagnóstico assistido estão enfrentando adversarial inputs
físicos — perturbações imperceptíveis ao olho humano em
imagens médicas que fazem o modelo classificar erroneamente.
Um threat model que não inclui esse vetor específico para
modelos de visão computacional em saúde está incompleto —
e um profissional que não sabe que ele existe não está
à frente do adversário.

---

### Função 8 — Governança, Risco e Conformidade

**O que é:**
Garantir que modelos e pipelines estão em conformidade com
a regulação vigente, com riscos formalmente gerenciados e
com evidências auditáveis para qualquer fiscalização.
Conformidade não é burocracia — é o que permite que o negócio
continue operando quando o regulador bate à porta.

**O que precisa saber:**
No ecossistema financeiro brasileiro:
— CMN 5.274/2025: governança de risco, responsabilidade
formal da alta gestão sobre sistemas de ML que afetam
decisões financeiras
— BCB 538/2025: controles de segurança cibernética exigidos
de todas as IFs, incluindo pipelines de ML em produção
— IN BCB 587/2025: auditabilidade e rastreabilidade de modelos
ML usados em antifraude — um modelo comprometido via supply
chain viola essa norma diretamente
— LGPD: base legal para dados de treino, pseudonimização
obrigatória de dados pessoais, RIPD para modelos que processam
dados sensíveis, notificação à ANPD em até 72h em caso
de incidente com dados pessoais
Em outros ecossistemas: mapear a regulação equivalente
antes de qualquer outra ação. Para healthtech: LGPD aplicada
a dados sensíveis de saúde, CFM para sistemas de apoio
a diagnóstico, ANVISA para softwares com função de dispositivo
médico (SaMD). Para varejo e consumo: LGPD aplicada a dados
comportamentais, CDC para modelos de precificação dinâmica.
Como classificar dados por sensibilidade e definir o
tratamento correto para cada categoria.
Como documentar decisões de modelo de forma auditável —
não só o que o modelo decide, mas por que foi treinado
daquela forma, com quais dados e quem aprovou.
Como gerar evidências de controles para auditorias internas
e externas que respondam perguntas reais de reguladores.
Como comunicar postura de risco para C-level e board em
linguagem de negócio sem perder precisão técnica.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: em 2025 e 2026, o BCB intensificou
as visitas técnicas a fintechs para avaliar a conformidade
de modelos de antifraude e score de crédito com a IN BCB
587/2025. Fintechs que não conseguem apresentar em horas
a documentação de rastreabilidade de decisões de modelo
estão sujeitas a multas e a restrições operacionais que
afetam diretamente a licença de funcionamento. Quando o
Banco Central agenda uma visita técnica com 48h de aviso,
você já tem toda a documentação organizada e auditável —
não precisa de uma semana de correria para montar o que
deveria existir desde o primeiro deploy.

Contexto universal: a União Europeia implementou em 2026
os primeiros requisitos obrigatórios do AI Act para sistemas
de alto risco — incluindo modelos de crédito, emprego e
saúde. Empresas com operações na Europa ou que processam
dados de cidadãos europeus precisam de conformidade
documentada. O profissional que entende como mapear
obrigações regulatórias e transformar em controles
implementados é o que permite que o negócio expanda
para novos mercados sem risco regulatório.

---

### Função 9 — Arquitetura e Engenharia de Segurança

**O que é:**
Projetar e implementar os controles técnicos que tornam
o ambiente de ML seguro por construção — não por revisão
posterior. Segurança que precisa ser adicionada depois
é sempre mais cara, mais frágil e mais incompleta do que
segurança projetada desde o início.

**O que precisa saber:**
Como hardening de CI/CD funciona na prática: GitHub Actions
com OIDC efêmero (sem tokens permanentes), branch protection
com block force push obrigatório, CODEOWNERS para controle
de quem pode alterar arquivos críticos, commits assinados
com GPG.
Como gerenciar secrets com Vault, GCP Secret Manager ou
AWS Secrets Manager — nunca em variáveis de ambiente
não gerenciadas, nunca em repositórios, nunca em
arquivos .env commitados.
Como construir containers seguros: imagem base pinada por
SHA imutável (não :latest), SBOM gerado no build,
Cosign para assinatura, Trivy para scan de vulnerabilidades
antes do push para o registry.
Como configurar Kubernetes com Pod Security Admission
e seccomp profiles — limitando o que cada container
pode fazer no sistema operacional.
Como implementar egress filtering: serviços de ML só se
comunicam com endpoints autorizados — um setup.py que
tenta chamar api.mainnet-beta.solana.com é bloqueado
automaticamente, como o Harden-Runner da StepSecurity
demonstrou com o GlassWorm.
Como aplicar IAM com menor privilégio em cloud para cada
componente do pipeline — o serviço de inferência não
precisa de permissão de escrita no model registry.
Como usar SLSA nível 3+ para garantir proveniência
de artefatos — cada modelo em produção tem uma cadeia
de custódia verificável desde o código até o deploy.
Como integrar ferramentas de detecção (Falco, OPA/Gatekeeper)
no ambiente de produção para detectar comportamento anômalo
em runtime.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: em 2026, o Banco Central começou a
incluir avaliação de controles de CI/CD e gestão de secrets
nas visitas técnicas a IFs — especificamente após incidentes
de supply chain que comprometeram pipelines de dados de
open finance. Quando um penetration test externo contratado
pelo conselho tenta comprometer o pipeline de ML e encontra
resistência estrutural em cada camada — egress filtering
bloqueando chamadas anômalas, tokens efêmeros que expiram
em minutos, artefatos assinados que rejeitam qualquer
versão não verificada — o relatório do pentest se torna
o argumento mais forte para o orçamento de segurança
do próximo ano.

Contexto universal: em 2026, ataques a pipelines de CI/CD
representam o vetor de comprometimento mais comum em
empresas de tecnologia segundo o relatório State of Software
Supply Chain da Sonatype. Arquitetura de segurança bem
implementada é o que separa empresas que descobrem o
comprometimento em minutos das que descobrem em meses —
ou nunca descobrem.

---

### Função 10 — Detecção, Resposta e Recuperação

**O que é:**
Monitorar continuamente, detectar anomalias antes que virem
incidentes, responder com precisão quando o incidente acontece
e aprender estruturadamente com cada ocorrência para que
o mesmo problema não aconteça duas vezes.

**O que precisa saber:**
Como construir monitoramento integrado que cobre pipeline
e modelo simultaneamente — a mesma anomalia pode ser sinal
de problema operacional ou de ataque, e diferenciar os dois
exige contexto de ambas as camadas.
Como integrar telemetria de pipeline ao SIEM corporativo
com alertas diferenciados por severidade — não todo alerta
é incidente, e treinar o time a ignorar alertas de baixa
qualidade é tão perigoso quanto não ter alerta nenhum.
Como identificar a diferença entre drift natural de dados
e sinal de ataque adversarial — a pergunta "o modelo degradou
ou está sendo atacado?" tem respostas técnicas diferentes
e respostas de negócio completamente diferentes.
Como executar rollback seguro de modelo comprometido sem
interromper o serviço — trocar o modelo em produção por uma
versão anterior validada enquanto o serviço continua
respondendo requests.
Como conduzir post-mortem estruturado que gera aprendizado
real — não um relatório de culpabilidade, mas um documento
de sistema que identifica onde o processo falhou e o que
muda para que não falhe de novo.
Como comunicar incidente para stakeholders, C-level e
reguladores com a linguagem e o timing corretos para
cada audiência — o BCB tem prazo de notificação de incidente
que não pode ser perdido, e a linguagem para o Banco Central
é diferente da linguagem para o CEO e diferente da linguagem
para o time técnico.

**Como o serviço é reconhecido pelos superiores:**
Contexto financeiro: em fevereiro 2026, uma fintech brasileira
de médio porte teve seu modelo de antifraude do PIX
comprometido via ataque de data poisoning — transações
fraudulentas específicas foram sendo marcadas como legítimas
de forma gradual, abaixo do threshold de detecção de drift.
O ataque ficou ativo por 11 dias antes de ser detectado
por monitoramento de business metrics (taxa de chargebacks
subindo acima do esperado). O custo foi de R$2,3 milhões
em fraudes aprovadas indevidamente mais a notificação
obrigatória ao BCB e à ANPD. Um MLSecOps Engineer com
monitoramento de input distribution bem configurado teria
detectado a anomalia nos primeiros 2 dias — antes de qualquer
impacto financeiro material. Quando o CEO pergunta depois
de um incidente "por que não detectamos antes?", a resposta
não pode ser "não tínhamos o monitoramento certo". Precisa
ser "detectamos em X horas, contemos em Y minutos,
aqui está o post-mortem e aqui está o que mudou".

Contexto universal: em 2026, o tempo médio para detecção
de comprometimento de modelos de ML em produção é de
23 dias segundo o relatório IBM Cost of Data Breach 2025.
Cada dia de modelo comprometido em produção é um dia
de decisões incorretas sendo tomadas em escala. Detecção
em horas em vez de semanas é o diferencial que transforma
um incidente controlado em crise evitada.

---

## O Momento Exato de Entrada em Cada Fase

```
CONCEPÇÃO DO PROJETO
├── Outros: definem problema de negócio, escolhem abordagem ML
└── MLSecOps: threat modeling, requisitos de segurança,
    classificação de dados, definição de controles necessários,
    avaliação de viabilidade regulatória antes de uma linha
    de código existir

DESENVOLVIMENTO
├── Outros: escrevem código, fazem experimentos, treinam modelos
└── MLSecOps: ambiente de dev seguro, CI/CD com controles
    integrados desde o início, auditoria contínua de
    dependências, linhagem de dados documentada,
    reprodutibilidade garantida

EXPERIMENTAÇÃO E VALIDAÇÃO
├── Outros: avaliam métricas, ajustam modelo
└── MLSecOps: adversarial testing, model inversion testing,
    validação de integridade do artefato gerado,
    verificação de data leakage no experimento,
    avaliação de fairness e viés que podem criar
    risco regulatório em produção

REGISTRO E PROMOÇÃO PARA PRODUÇÃO
├── Outros: registram modelo, solicitam aprovação de deploy
└── MLSecOps: gate formal — valida proveniência e assinatura
    do artefato, conformidade regulatória documentada,
    evidências de testes adversariais realizados,
    aprova ou bloqueia com justificativa registrada

PRODUÇÃO E MONITORAMENTO CONTÍNUO
├── Outros: acompanham métricas de negócio e performance
└── MLSecOps: monitoramento adversarial e operacional
    integrados, detecção de anomalias em input/model/business,
    resposta a incidentes com playbooks definidos,
    evidências auditáveis geradas continuamente,
    ciclo de retreino seguro quando necessário
```

***

## Como o Papel Varia por Tipo de Empresa

O papel é o mesmo em qualquer empresa.
O que muda é a velocidade, a formalidade e a profundidade
regulatória exigida.

**Banco grande (Itaú, Bradesco, Caixa, Santander BR)**
Gates formais em cada fase com aprovação documentada em sistema.
Modelos que afetam crédito, antifraude ou open finance têm
exigência regulatória de documentação prévia pelo BCB.
O MLSecOps Engineer é consultado antes mesmo da concepção
do projeto — não depois que o modelo já foi treinado.
Auditoria interna e externa é constante e as 10 funções
precisam ter evidências geradas continuamente.
Velocidade menor, exigência de rastreabilidade máxima,
tolerância zero para gaps de conformidade.

**Fintech de crescimento rápido (Nubank, PicPay, Stone, Inter)**
Pipeline move mais rápido e o MLSecOps Engineer precisa
equilibrar velocidade com controle sem virar gargalo.
Segurança como código no CI/CD substitui aprovação manual
em cada commit — os gates automáticos precisam ser tão
rigorosos quanto os manuais de banco grande, mas invisíveis
no fluxo normal de desenvolvimento.
O desafio específico aqui é crescimento de base que acelera
o concept drift — o modelo treinado com 500 mil clientes
se comporta diferente quando a base chega em 5 milhões.
Monitoramento e retreino precisam escalar junto com o negócio.

**TechFin (Mercado Pago, Amazon Pay, iFood Pay)**
Empresas de tecnologia que adicionaram serviços financeiros
têm o desafio de cultura de tech company (velocidade, deploy
contínuo) com obrigações de IF (conformidade, rastreabilidade).
O MLSecOps Engineer é muitas vezes o profissional que cria
a ponte entre as duas culturas — traduzindo exigências do BCB
em controles técnicos que o time de engenharia consegue
implementar sem freiar o ritmo de produto.

**Healthtech**
O custo de um modelo comprometido pode ser vida humana —
não só dinheiro ou reputação. O MLSecOps Engineer entra
na concepção para mapear risco clínico de manipulação
adversarial e para garantir que dados de saúde recebem
o tratamento que a LGPD exige para dados sensíveis.
Em 2026, a ANVISA começou a exigir documentação de
validação de segurança para softwares com função de
dispositivo médico (SaMD) que usam ML — o profissional
que entende tanto o lado técnico quanto o regulatório
é raro e estratégico.

**Startup early stage (qualquer setor)**
Frequentemente não tem pipeline estruturado nem cultura
de segurança estabelecida. O MLSecOps Engineer entra e
constrói a fundação segura do zero — não confere algo
existente, projeta como deve ser para que quando crescer
já tenha os controles certos desde a origem.
Aqui o impacto de longo prazo é o maior de todos —
o custo de corrigir arquitetura ruim cresce exponencialmente
com o tamanho da empresa. Construir certo desde o início
é sempre mais barato do que refatorar segurança em um
sistema que já está em produção com milhares de usuários.

***

## O Que o MLSecOps Engineer Precisa Para Ser Reconhecido

Conhecimento técnico sozinho não constrói reconhecimento.
O que constrói é a combinação de quatro dimensões simultâneas:

**Dimensão 1 — Saber técnico profundo nas duas metades**
Dominar MLOps e Security com profundidade suficiente para
implementar, avaliar e evoluir — não apenas citar frameworks
e ferramentas. Saber por que cada controle existe, o que
ele protege, onde ele falha e o que acontece quando não
está presente. Entender como as duas metades se afetam —
uma decisão de arquitetura de pipeline tem implicações
de segurança, e uma decisão de segurança tem implicações
de operação.

**Dimensão 2 — Raciocínio adversarial**
Pensar como o atacante antes de pensar como o defensor.
Para cada sistema, pipeline ou modelo: o que um adversário
buscaria aqui? Por onde entraria? O que exploraria primeiro?
Em 2026, esse adversário pode estar usando IA para automatizar
o reconhecimento e a exploração — o raciocínio adversarial
precisa incluir essa camada.
Sem essa dimensão, os controles implementados protegem
o que parece importante — não o que o adversário vai
atacar de fato.

**Dimensão 3 — Inteligência de negócio**
Entender o business profundamente o suficiente para saber
o que proteger com prioridade e o que operar com excelência.
Num banco, o modelo de antifraude do PIX é mais crítico
que o modelo de recomendação de produtos financeiros —
e os dois têm requisitos operacionais e de segurança
completamente diferentes.
Numa healthtech, o modelo de triagem tem risco de vida
que nenhuma métrica de F1 captura — e esse risco precisa
estar no threat model, no monitoramento e no plano de
resposta a incidentes.
Sem essa dimensão, o trabalho é tecnicamente correto
e estrategicamente irrelevante.

**Dimensão 4 — Comunicação de valor**
Traduzir o trabalho técnico em linguagem que CEO, CTO,
CFO e board entendem e valorizam.

Não: *"implementamos SLSA nível 3 e egress filtering
no CI/CD com OIDC efêmero"*

Mas: *"garantimos que nenhum artefato de modelo pode ser
substituído por uma versão comprometida sem que o sistema
detecte e bloqueie automaticamente — eliminando o vetor
de ataque que custou R$2,3 milhões a uma fintech brasileira
em fevereiro de 2026 e gerou notificação obrigatória
ao Banco Central"*

Sem essa dimensão, o trabalho excelente permanece invisível
para quem decide promoção, orçamento e estratégia.

***

## O Princípio Central do Papel

O MLSecOps Engineer de excelência em 2026 não é reconhecido
porque resolveu muitos incidentes.

É reconhecido porque os incidentes que poderiam ter acontecido
não aconteceram — e quando acontecem, são resolvidos com uma
precisão que demonstra que o sistema foi construído para isso.

A excelência neste papel é medida pelo que não explode,
pelo modelo que não foi comprometido, pela fraude que não
passou, pelo regulador que foi atendido sem correria e
pelo pipeline que continuou funcionando quando deveria.

Comunicar esse valor de forma que superiores entendam
e valorizem é tão importante quanto o trabalho técnico
que o produz — porque trabalho invisível não constrói carreira,
não garante orçamento e não protege o profissional quando
as prioridades da empresa mudam.

***

*Criado em: março 2026*
*Repositório: mlsecops-playbook (privado)*
*Localização: fase-1-identidade/papel-e-funcoes.md*
*Atualizar quando o escopo do papel evoluir ou quando novo*
*tipo de business relevante for incorporado ao sistema*
