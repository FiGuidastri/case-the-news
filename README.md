# Palavritas — o que faz um jogador voltar?

Case prático para o processo seletivo de **Analista de Dados — Produto & Growth** do the news. O desafio original está em [CASE.md](CASE.md); este repositório é a entrega.

**Pergunta do Head de Produto:** *"O que está determinando se um usuário volta a jogar — e o que podemos fazer para aumentar isso?"*

## TL;DR

1. **Não é "quem" joga que importa, é "quando" e "quanto" essa pessoa está conectada com o the news.** Setor, salário, cargo e até aparelho não fazem diferença na retenção.
2. **Dois fatores se destacam:** jogar de manhã e abrir a newsletter antes de jogar — ambos associados a uma retenção de 30 dias bem mais alta, confirmados por mais de uma fonte de dado.
3. **Voltar no dia seguinte é o ponto fraco:** nenhum fator medido explica isso hoje — é a oportunidade central das propostas.

Resultado completo, com diagnóstico dos dados, achados e 3 propostas testáveis, em [RELATORIO_ANALISE.pdf](RELATORIO_ANALISE.pdf).

## Como navegar este repositório

| Se você quer... | Vá para |
| --- | --- |
| Ler o resultado | [RELATORIO_ANALISE.pdf](RELATORIO_ANALISE.pdf) (ou [.md](RELATORIO_ANALISE.md)) |
| Ver o código: limpeza, testes estatísticos, geração dos gráficos | [main.ipynb](main.ipynb) |
| Explorar os dados interativamente (KPIs, retenção, perfil dos usuários) | [dashboard.html](dashboard.html) — abrir direto no navegador, não precisa de servidor |
| Entender o desafio original e os dados recebidos | [CASE.md](CASE.md) |

## Estrutura

```
data/                   3 CSVs originais (sessions, attempts, user_profile)
imgs/                   gráficos usados no relatório
main.ipynb              limpeza, diagnóstico e análise estatística, passo a passo
RELATORIO_ANALISE.md    relatório para o Head de Produto (fonte)
RELATORIO_ANALISE.pdf   o mesmo relatório, formatado para leitura/impressão
dashboard.html          dashboard interativo (Chart.js), autocontido
CASE.md                 enunciado original do case
```

## Como rodar localmente

```bash
pip install -r requirements.txt
jupyter notebook main.ipynb
```

O notebook lê os CSVs direto de `data/` (caminhos relativos) e está organizado em 3 partes, na mesma ordem do case: **limpeza e diagnóstico**, **análise** e **proposta**.

> Os dados são sintéticos (não reais) — ver aviso em [CASE.md](CASE.md).
