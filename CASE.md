# Case Processo Seletivo — Analista de Dados Produto & Growth

## Sobre o processo

Este case é a etapa prática do processo seletivo para **Analista de Dados — Produto & Growth** do the news.

Você terá **5 dias corridos** para entregar. Estimativa de dedicação: **4 a 6 horas**. Não avaliamos só o resultado — avaliamos o raciocínio, como você lida com dados imperfeitos e se você transforma análise em ação.

Ferramenta livre: SQL, Python, R, Excel — use o que você trabalha melhor.

---

## Sobre o the news

O the news é a maior newsletter de notícias do Brasil, com mais de 2 milhões de assinantes. Temos também um app com funcionalidades de engajamento diário.

Uma dessas features é o **Palavritas** — nosso jogo de palavras diário, estilo Wordle em português. Todo dia uma palavra nova de 5 letras. O leitor tem até 6 tentativas para acertar. A pergunta que move o time: **quem joga, quem volta, e o que prediz isso?**

---

## O dataset

Você vai receber **3 arquivos** com dados de comportamento do Palavritas e perfil dos usuários.

**→ Acessar dataset aqui**

O arquivo tem 3 abas: `palavritas_sessions`, `palavritas_attempts` e `user_profile`. Você pode exportar cada aba como CSV ou trabalhar direto no Sheets.

### palavritas_sessions.csv (~41.000 linhas)

| Coluna | Descrição |
| --- | --- |
| `session_id` | Identificador único da sessão de jogo |
| `user_id` | Identificador anonimizado do usuário |
| `word` | Palavra do desafio do dia |
| `word_date` | Data do desafio |
| `attempts` | Número de tentativas (1–6) |
| `result` | Resultado: `win` / `lose` |
| `time_to_complete_sec` | Tempo de jogo em segundos |
| `device` | Dispositivo usado |
| `session_hour` | Hora do dia em que jogou (0–23) |
| `streak_day` | Dia atual da sequência do usuário |
| `played_next_day` | Se o usuário voltou a jogar no dia seguinte |
| `newsletter_open_before_game` | Se abriu a newsletter antes de jogar naquele dia |
| `active_d30` | Se o usuário estava ativo 30 dias após essa sessão |

### palavritas_attempts.csv (~149.000 linhas)

| Coluna | Descrição |
| --- | --- |
| `session_id` | FK para sessions |
| `attempt_number` | Número da tentativa |
| `guess` | Palavra digitada |
| `correct_letters` | Letras certas em posição errada |
| `correct_positions` | Letras certas na posição certa |

### user_profile.csv (800 linhas — usuários que responderam pesquisa)

| Coluna | Descrição |
| --- | --- |
| `user_id` | FK para sessions |
| `age_range` | Faixa etária |
| `state` | Estado (UF) |
| `city` | Cidade |
| `salary_range` | Faixa salarial |
| `job_role` | Cargo |
| `sector` | Setor de trabalho |
| `company_size` | Porte da empresa |
| `orders_food_delivery` | Se pede comida por app |
| `food_delivery_freq_week` | Quantas vezes por semana |
| `food_delivery_platform` | Plataforma usada |
| `primary_device` | Dispositivo principal |
| `plays_other_word_games` | Se joga outros jogos de palavras |
| `typical_play_time` | Período típico de jogo (morning/afternoon/evening/night) |
| `newsletter_subscriber` | Se é assinante da newsletter |

> ⚠️ **Atenção:** os dados não são reais.
> 

---

## O desafio

Você recebeu esses dados e tem uma reunião com o Head de Produto na segunda-feira. Ele quer saber:

> *"O que está determinando se um usuário volta a jogar — e o que podemos fazer para aumentar isso?"*
> 

### Entrega 1 — Limpeza e diagnóstico

Antes de qualquer análise: o que você encontrou de problemático nesse dataset? O que limpou, o que descartou e por quê?

Documente as decisões — não entregue só o dado limpo.

### Entrega 2 — Análise

Quais variáveis mais se correlacionam com o usuário estar ativo no D30 e voltar a jogar no dia seguinte?

Explore pelo menos: horário de jogo, palavra do dia, perfil do usuário (setor, salário, device), frequência de food delivery, e relação com a newsletter.

Traga queries/código e o raciocínio de cada etapa — não só o resultado.

### Entrega 3 — Proposta

Com base no que você encontrou: **o que você mudaria ou testaria no Palavritas na próxima semana?**

Formato:

- **Hipótese:** "Acredito que X porque Y"
- **Ação:** proposta concreta
- **Critério de sucesso:** "Saberei que funcionou quando Z"

*Quem para na análise sem chegar na proposta não está no perfil que buscamos.*

---

## Entregáveis

1. **Código ou queries** (`.sql`, `.py`, `.ipynb`, Google Colab, ou similar)
2. **Documento de análise** com diagnóstico, achados e proposta — escrito para que o Head de Produto entenda sem tradução técnica

### Bônus

- Dashboard no Metabase, Looker Studio ou similar
- Análise de significância estatística dos achados

---

## O que vamos avaliar

| Critério | O que estamos vendo |
| --- | --- |
| **Limpeza** | Identificou e tratou os problemas antes de analisar? Documentou as decisões? |
| **Raciocínio analítico** | Foi além do óbvio? Questinou a pergunta antes de responder? |
| **Comunicação** | O documento pode ser lido pelo Head de Produto sem jargão técnico? |
| **Propositivo** | Chegou em uma recomendação com hipótese e critério de sucesso? |
| **Profundidade** | Explorou múltiplas variáveis ou ficou só na superfície? |

---

## Como entregar

Preencha o formulário com os links dos seus entregáveis:

**→ Acessar formulário de entrega**

**Prazo:** June 29, 2026

---

> Dúvidas sobre os dados? Não respondemos — faz parte da avaliação como você lida com ambiguidade.
>