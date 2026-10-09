# Estrutura do repositório

Referência de organização para o Tech Challenge — Fase 2: estrutura de diretórios,
README, `requirements.txt` e organização geral do repositório.

## Template, no momento do clone

```
.
├── .gitignore
├── CHECKLIST.md
├── ESTRUTURA.md
├── README.md
├── requirements.txt
├── data
│   ├── README.md
│   ├── raw
│   │   └── .gitkeep
│   └── processed
│       └── .gitkeep
├── docs
│   └── README.md
└── notebooks
    ├── 01_eda.ipynb
    ├── 02_preprocessamento.ipynb
    ├── 03_modelagem.ipynb
    ├── 04_avaliacao.ipynb
    └── README.md
```

## O mesmo repositório, no momento da entrega

Nomes de arquivo são ilustrativos, mas a organização deve ser esta.

```
.
tech-challenge-fase2-grupo28/
├── .gitignore
├── CHECKLIST.md
├── ESTRUTURA.md
├── README.md
├── requirements.txt
│
├── data/
│   ├── README.md
│   ├── raw/                           Dados originais, não versionados
│   └── processed/                     Dados processados, não versionados
│
├── docs/
│   ├── README.md
│   └── Apresentação Risco de Crédito 0 Tech Challenge Grupo 28.pdf
│
├── notebooks/
│   ├── README.md
│   └── Tech_Challenge_grupo28_v3.ipynb
│
└── results/
    ├── figures/
    │   ├── curva_precision_recall.png
    │   ├── curva_roc.png
    │   ├── distribuicao_bons_maus_pagadores.png
    │   ├── distribuicao_idade_classificacao.png
    │   ├── distribuicao_renda_transformada.png
    │   ├── distribuicao_status_credito.png
    │   ├── matriz_confusao_logistica.png
    │   ├── matriz_confusao_random_forest.png
    │   ├── permutation_importance_logistica.png
    │   └── taxa_maus_pagadores_tipo_renda.png
    │
    ├── metrics/
    │   ├── importancia_variaveis_logistica.csv
    │   ├── metricas_modelos.csv
    │   └── predicoes_random_forest.csv
    │
    └── models/
        └── modelo_logistic_regression.joblib

**Observações sobre a organização**

O projeto utiliza um notebook principal, em vez de quatro notebooks numerados.
Os dados originais e processados não são incluídos no versionamento.
Os gráficos, as métricas e o modelo treinado estão organizados na pasta results/.
O modelo salvo permite reutilizar a pipeline treinada sem executar novamente todas as etapas de treinamento, desde que o ambiente e as dependências sejam compatíveis.
A estrutura documenta a organização atual do projeto, sem implicar que todas as convenções do template original tenham sido adotadas.
```

## Convenções

| Regra | Motivo |
|---|---|
| Notebooks numerados `01_` … `04_` | a ordem de leitura vira a ordem de execução |
| Nada de dataset em `data/` no Git | repositório leve e licença da fonte respeitada |
| Saídas dos gráficos salvas nos notebooks | o avaliador vê os resultados sem rodar nada |
| Modelos `.pkl` fora do Git | são reproduzíveis a partir do código |
| `RANDOM_STATE = 42` na primeira célula de cada notebook | mesmo número em toda execução |
| `snake_case`, sem acento e sem espaço em nomes de arquivo | compatibilidade entre Windows, macOS e Linux |
| Uma branch por integrante, merge via PR em `main` | histórico legível e trabalho paralelo sem conflito |

## Erros mais comuns

1. **Repositório privado.** Inviabiliza a avaliação da entrega. Verifique em janela anônima.
2. **README com `<!-- PREENCHER -->`.** Sinaliza entrega inacabada antes mesmo da análise.
3. **Notebook com células fora de ordem** (`[7]`, `[2]`, `[15]`). Indica que o resultado
   não é reproduzível.
4. **Notebook commitado sem as saídas.** O avaliador abre e não vê gráfico nenhum.
5. **`requirements.txt` genérico**, copiado de outro projeto, listando o que não foi usado.
6. **Gráficos sem interpretação.** Um gráfico sem leitura não comunica nada.
7. **Dataset de 200 MB commitado** em `data/raw/`.
