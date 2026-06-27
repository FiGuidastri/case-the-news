# Palavritas: o que faz um jogador voltar?

**Para:** Head de Produto
**Sobre:** Análise dos dados do Palavritas — diagnóstico, achados e proposta
**Pergunta original:** *"O que está determinando se um usuário volta a jogar — e o que podemos fazer para aumentar isso?"*

> O código completo, com cada etapa de limpeza e cada teste estatístico, está no notebook `main.ipynb`. Este documento traz o resultado, sem o passo a passo técnico.

---

## Resumo em 3 frases

1. **Não é "quem" joga que importa, é "quando" e "quanto" essa pessoa está conectada com o the news.** Setor, salário, cargo e até aparelho (Android x iOS) não fazem diferença na retenção.
2. **Dois fatores se destacam com força:** jogar de manhã, e abrir a newsletter antes de jogar. Os dois aparecem associados a uma retenção de 30 dias bem mais alta — e cada um confirmado de mais de uma forma na base.
3. **Voltar no dia seguinte é o ponto fraco:** nenhum fator que medimos explica isso hoje. É uma oportunidade de criar um gatilho que ainda não existe no produto (proposta 3, abaixo).

---

## 1. Diagnóstico — em que estado os dados chegaram

Antes de analisar qualquer coisa, fui atrás de problemas nos três arquivos recebidos. Resumo do que encontrei e do que decidi fazer:

- **~3% das sessões de jogo estavam duplicadas** (a mesma partida registrada duas vezes) — removidas.
- **O mesmo aparelho aparecia escrito de 6 formas diferentes** (`iOS`, `IOS`, `ios`, `Android`, `ANDROID`, `android`) — padronizado para 2 categorias.
- **63 sessões não tinham resultado registrado** (nem vitória, nem derrota). Quase todas tinham zero tentativas e tempo de jogo zerado ou negativo — sinal de que a pessoa abriu o jogo e não chegou a jogar. Tratei como uma categoria própria ("incompleta"), em vez de contar como derrota.
- **90 sessões registravam um número de tentativas impossível** (0, 7 ou 8 — o jogo permite no máximo 6). Mantive a sessão (porque o restante dos dados dela é válido), mas sinalizei esse campo específico como não confiável.
- **43 sessões tinham tempo de jogo negativo ou zero** — erro de captura, tratado como dado ausente.
- **No arquivo de tentativa-a-tentativa**, havia tentativas duplicadas e tentativas fora da regra do jogo (mais de 6 por partida, ou palpites com 4 ou 6 letras em vez de 5) — no total, cerca de 1,2% das linhas, removidas.
- **Cargos e funções dos usuários estavam escritos com grafias diferentes** (`Consultor` e `consultor` contados como cargos diferentes) — padronizado.
- **Entre 15% e 37% dos 800 perfis não informaram idade, cidade ou faixa salarial** na pesquisa — mantive como "não informado" em vez de inventar um valor, para não distorcer a análise.
- **O ponto mais importante: 1 em cada 3 jogadores (400 de 1.200) não tem perfil preenchido.** O perfil vem de uma pesquisa respondida voluntariamente, então os 800 que responderam provavelmente não representam todo mundo que joga — é razoável supor que sejam os mais engajados. Por isso, separei a análise em duas partes: uma com todos os jogadores (sem dado de perfil), e outra só com quem respondeu a pesquisa — e tratei essa segunda parte como válida apenas para esse grupo, não para a base inteira.

---

## 2. O que descobrimos

Eu olhei dois comportamentos de retorno:

- **Voltar no dia seguinte** ao jogo.
- **Continuar ativo 30 dias depois** dessa sessão.

E testei se cada um desses comportamentos varia de forma consistente (não por acaso) segundo: horário de jogo, dia da semana, aparelho, dificuldade da palavra, abertura da newsletter, e — para quem tem perfil — setor, cargo, salário, porte da empresa, hábito de delivery e assinatura da newsletter.

### Voltar no dia seguinte: nenhum fator se destacou

Testamos tudo que a base permite — nada explica de forma relevante por que um jogador volta ou não no dia seguinte. Isso não é um problema da análise: é um achado em si. **Hoje o produto não tem nenhum gatilho identificável de curtíssimo prazo** que traga o jogador de volta logo no dia seguinte. Trato isso como uma oportunidade (proposta 3).

### Continuar ativo depois de 30 dias: dois fatores fortes

| Fator | O que vimos |
|---|---|
| **Horário do jogo** | Quem joga de manhã tem entre 35% e 38% de chance de continuar ativo 30 dias depois — bem acima dos 28% a 30% de quem joga em outros horários. É a diferença mais forte de toda a análise, e aparece tanto no horário real de cada partida quanto no horário que a própria pessoa diz preferir — duas fontes de dado apontando para o mesmo padrão. |
| **Abrir a newsletter antes de jogar** | Quem abre a newsletter do the news antes de jogar naquele dia tem 38% de retenção em 30 dias, contra 30% de quem não abre — um salto de quase 1/4. Isso vale para o comportamento real do dia (abriu ou não a newsletter antes de jogar); só "ser assinante" da newsletter, sem necessariamente abrir, não faz tanta diferença. |
| *(secundário)* Pedir comida por aplicativo | Quem pede comida por delivery tende a voltar um pouco mais no dia seguinte (18,5% vs 16%), mas o efeito é pequeno — não tratamos como prioridade. |

### O que não importa (e isso também é informação valiosa)

Setor de trabalho, faixa salarial, porte da empresa, cargo, aparelho usado (Android x iOS), plataforma de delivery, e até **quão bem a pessoa joga** (se venceu ou perdeu, quantas tentativas usou, quanto tempo levou) — nada disso muda a chance de a pessoa voltar a jogar. O retorno não depende do desempenho no jogo nem do perfil de quem joga.

---

## 3. O que eu proponho testar

### Proposta 1 — Empurrar o jogo para a manhã

- **Hipótese:** jogar de manhã ancora o Palavritas numa rotina diária que já existe (café, trajeto, início do expediente). Rotinas matinais são mais estáveis que hábitos noturnos, por isso vemos mais retenção em quem joga de manhã.
- **Ação:** lembrete (push ou destaque na newsletter da manhã) sobre o desafio do dia, enviado nas primeiras horas, para o grupo que hoje joga à tarde ou à noite.
- **Critério de sucesso:** o grupo que recebeu o lembrete passa a ter uma retenção de 30 dias visivelmente maior que um grupo parecido que não recebeu — testado em A/B, não só observado.

### Proposta 2 — Aproximar Palavritas e newsletter

- **Hipótese:** abrir a newsletter antes de jogar é sinal de um jogador mais conectado com o the news como um todo — e reforçar essa ponte deve aumentar a chance de ele voltar.
- **Ação:** CTA mais visível para o Palavritas dentro da newsletter diária, e um lembrete pelo app pouco depois do horário em que cada pessoa costuma abrir a newsletter.
- **Critério de sucesso:** mais pessoas passam a abrir a newsletter antes de jogar, **e** esse grupo mantém uma retenção de 30 dias acima de um grupo controle que não recebeu o CTA.

### Proposta 3 — Criar um gatilho para o retorno no dia seguinte

- **Hipótese:** hoje não existe nenhum gatilho de curto prazo no produto — é por isso que nada explica quem volta no dia seguinte. Criar um gatilho explícito deve mudar esse número.
- **Ação:** notificação de "sequência em risco" (streak), avisando que a sequência do jogador se perde se ele não jogar hoje, enviada no horário em que ele costuma jogar.
- **Critério de sucesso:** a taxa de retorno no dia seguinte sobe de forma visível e estatisticamente confiável no grupo que recebeu a notificação, comparado a um grupo controle.

---

## Limitações a ter em mente

- Um terço dos jogadores não tem perfil preenchido — qualquer achado sobre perfil vale para quem respondeu a pesquisa, não necessariamente para todo mundo.
- Os achados são de **associação, não de causa comprovada.** Jogar de manhã e abrir a newsletter podem ser causa, consequência, ou apenas marcadores de um terceiro fator (ex.: "o quanto a pessoa gosta do the news em geral"). É exatamente por isso que as três propostas acima são desenhadas como testes controlados (A/B), e não como mudanças direto em produção.
