# EDA — Wine Quality (UCI)

Análise exploratória do dataset Wine Quality da UCI, explorando distribuições, correlações, outliers e diferenças entre vinhos tintos e brancos.

## Sobre

Este notebook é a fonte técnica do post **"Análise Exploratória de Dados na prática: Wine Quality"** no blog [jlp-sistemas.com.br](https://jlp-sistemas.com.br/blog/ciencia-de-dados/eda-wine-quality).

## Para quem está começando

O notebook foi escrito para ser acompanhado por quem está iniciando em ciência de dados — não é preciso conhecimento prévio de estatística. Cada conceito (correlação, outlier, distribuição assimétrica, e assim por diante) é explicado em linguagem simples no momento em que aparece, antes do nome técnico ser usado, e há um mini-glossário logo no início para consulta.

## Dataset

- **Fonte:** [UCI Machine Learning Repository — Wine Quality](https://archive.ics.uci.edu/dataset/186/wine+quality)
- **Registros:** 6.497 (1.599 tinto + 4.898 branco)
- **Features:** 11 propriedades químicas + nota de qualidade (3–9)

## Como rodar

```bash
pip install -r requirements.txt
jupyter notebook notebooks/eda-wine-quality.ipynb
```

> Os dados são baixados automaticamente na primeira execução do notebook (salvos em `data/`, que está no `.gitignore`). Não é necessário baixar manualmente.

## Principais insights

1. **Dataset limpo, mas desbalanceado.** Não há valores nulos, mas a variável-alvo `quality` (a nota do vinho, de 3 a 9) está fortemente concentrada nas notas 5, 6 e 7 — mais de 93% dos registros. Notas extremas (3, 4, 8, 9) são raras. Isso é um desbalanceamento de classes: um modelo pode parecer bom só "chutando" as notas do meio, sem realmente aprender o que diferencia um vinho excelente de um mediano.
2. **Álcool é o preditor mais forte de qualidade — mas é uma relação moderada, não perfeita.** A correlação de Pearson mede o quanto duas variáveis andam juntas, numa escala de -1 (uma sobe enquanto a outra desce) a 1 (sobem sempre juntas); perto de 0, não há relação. O álcool tem 0,44 com `quality`, a correlação mais alta do dataset — um sinal claro, mas nenhuma variável sozinha explica a nota. Vinhos com nota ≥ 7 têm teor alcoólico médio de 11,43%, contra 10,26% dos demais.
3. **Densidade e acidez volátil puxam a nota para baixo — e isso não é "ruim", é só direção oposta.** Correlações de -0,31 e -0,27 com `quality`: quando essas variáveis sobem, a nota tende a cair. Densidade mais baixa está fisicamente ligada a mais álcool (correlação de -0,69 entre as duas, a mais forte do dataset), o que ajuda a explicar o padrão.
4. **Outlier não é sinônimo de erro.** Um outlier é um valor bem distante da maioria — mas não necessariamente um erro de medição. Valores extremos em `residual sugar` (açúcar residual), `chlorides` (cloretos) e nas variáveis de dióxido de enxofre provavelmente refletem estilos legítimos de vinho (vinhos doces, escolhas de conservação do produtor). Remover automaticamente esses pontos descartaria informação real sem justificativa técnica.
5. **Tinto e branco têm perfis químicos distintos.** O branco tem muito mais SO2 (dióxido de enxofre, usado para proteger o vinho da oxidação) — tanto livre quanto total — e mais açúcar residual; o tinto tem mais acidez volátil (associada a defeito de sabor, tipo gosto de vinagre, quando em excesso). Essa diferença sistemática é forte o suficiente para justificar usar o tipo do vinho como variável em um modelo.
6. **As features estão em escalas bem diferentes.** `chlorides` fica na casa dos centésimos (média de 0,056) enquanto `total sulfur dioxide` fica na casa das centenas (média de 115,7) — mais de mil vezes maior. Para explorar os dados isso não atrapalha, mas modelos sensíveis a escala (regressão logística, KNN, redes neurais) tendem a dar peso desproporcional às variáveis com números maiores, a menos que os dados sejam normalizados antes do treino.

Detalhes completos, gráficos e código estão em [`notebooks/eda-wine-quality.ipynb`](notebooks/eda-wine-quality.ipynb).

## Autor

**Jorge Leandro Piva** — Cientista de Dados Sênior
- [LinkedIn](https://www.linkedin.com/in/jorgelpiva)
- [Blog](https://jlp-sistemas.com.br/blog)
