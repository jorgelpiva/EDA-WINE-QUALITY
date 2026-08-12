# EDA — Wine Quality (UCI)

Análise exploratória do dataset Wine Quality da UCI, explorando distribuições, correlações, outliers e diferenças entre vinhos tintos e brancos.

## Sobre

Este notebook é a fonte técnica do post **"Análise Exploratória de Dados na prática: Wine Quality"** no blog [jlp-sistemas.com.br](https://jlp-sistemas.com.br/blog/ciencia-de-dados/eda-wine-quality).

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

1. **Dataset limpo, mas desbalanceado.** Não há valores nulos, mas a variável-alvo `quality` está fortemente concentrada nas notas 5, 6 e 7 (mais de 93% dos registros) — notas extremas (3, 4, 8, 9) são raras. Qualquer modelo preditivo vai precisar lidar com esse desbalanceamento.
2. **Álcool é o preditor mais forte de qualidade.** Correlação de Pearson de 0,44 com `quality`, a mais alta do dataset. Vinhos com nota ≥ 7 têm teor alcoólico médio de 11,43%, contra 10,26% dos demais.
3. **Densidade e acidez volátil pesam contra a nota.** Correlações de -0,31 e -0,27 com `quality`, respectivamente. Densidade mais baixa está fisicamente ligada a mais álcool (correlação de -0,69 entre as duas), o que ajuda a explicar o padrão.
4. **Outlier não é sinônimo de erro.** Valores extremos em `residual sugar`, `chlorides` e `sulfur dioxide` provavelmente refletem estilos legítimos de vinho (vinhos doces, escolhas de conservação) — remover automaticamente esses pontos descartaria informação real sem justificativa técnica.
5. **Tinto e branco têm perfis químicos distintos.** O branco tem muito mais SO2 (livre e total) e açúcar residual; o tinto tem mais acidez volátil. Essa diferença sistemática é forte o suficiente para justificar usar `tipo` como feature em um modelo.
6. **Escalas muito diferentes entre features.** De `chlorides` (~0,06) a `total sulfur dioxide` (~116), as variáveis estão em ordens de grandeza distintas — importante para qualquer etapa de modelagem futura.

Detalhes completos, gráficos e código estão em [`notebooks/eda-wine-quality.ipynb`](notebooks/eda-wine-quality.ipynb).

## Autor

**Jorge Leandro Piva** — Cientista de Dados Sênior
- [LinkedIn](https://www.linkedin.com/in/jorgelpiva)
- [Blog](https://jlp-sistemas.com.br/blog)
