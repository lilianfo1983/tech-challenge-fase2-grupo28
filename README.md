# Tech Challenge — Fase 2 | POSTECH Data Analytics

> **INSTRUÇÕES:** este README é um template. Substitua **todos** os blocos marcados com
> `<!-- PREENCHER -->` e apague as linhas de instrução antes de submeter.

---

| Campo | Valor |
|---|---|
| Turma | 2DTATBB |
| Grupo | 28|
| Data de entrega | 09/10/2026 |

### Integrantes

| Nome completo | RM | E-mail |
|---|---|---|
|Elisangela Freitas do Nascimento | RM377763 |efreitas7923@hotmail.com |
|Lilian Fonseca Oliveira | RM377750 |lilianfo@hotmail.com |
|Marcel e Silva de Almeida | RM377751 |marcel.shaka6@gmail.com |
|Michelle Ventura Oliveira Costa | RM377779 |michelle.ventura56@gmail.com |

## 2. Links da entrega

Estes três links são **obrigatórios** e devem ser idênticos aos do PDF de submissão.

| Item | Link |
|---|---|
| Repositório | https://github.com/lilianfo1983/tech-challenge-fase2-grupo28.git
| Vídeo executivo (≤ 5 min) | https://youtu.be/NZP1FulhNuY |
| Apresentação | [Apresentacao Risco Crédito -Tech Chalange Grupo28.pdf](https://github.com/lilianfo1983/tech-challenge-fase2-grupo28/blob/aed93386de07bff25ffab7f6473dd16c01fbd0b3/docs/Apresentacao%20Risco%20Cr%C3%A9dito%20-Tech%20Chalange%20Grupo28.pdf) |

> ⚠️ Repositório privado ou inacessível inviabiliza a avaliação da entrega.
> Confira o acesso em uma janela anônima antes de enviar.

---

## 3. O problema

A concessão de crédito é uma atividade estratégica para as instituições financeiras, pois possibilita ampliar o relacionamento com clientes e gerar receitas, mas também envolve o risco de inadimplência. A identificação de clientes com maior propensão a apresentar dificuldades de pagamento é, portanto, um desafio relevante para a gestão do risco de crédito.

A análise tradicional de crédito pode envolver um grande volume de informações cadastrais, pessoais, profissionais, financeiras e históricas, tornando relevante a utilização de técnicas de análise de dados e Machine Learning para identificar padrões associados ao comportamento de pagamento.

Neste projeto, o problema é abordado como uma tarefa de classificação supervisionada, com o objetivo de classificar clientes em dois grupos: bons pagadores e maus pagadores, conforme uma regra definida a partir do histórico de crédito disponível. Para isso, foram integradas informações cadastrais dos clientes e registros de seu histórico de crédito. A variável-alvo (TARGET) foi construída considerando a ocorrência de pelo menos um registro de atraso classificado entre os status de 1 a 5 no histórico observado.

Foram desenvolvidos e comparados diferentes algoritmos de classificação, incluindo Regressão Logística, Random Forest e Extra Trees, com o propósito de avaliar sua capacidade de identificar clientes associados ao risco de inadimplência. Como as classes apresentam distribuição desigual, a avaliação considera métricas como precisão, recall, F1-score, ROC-AUC, PR-AUC e acurácia balanceada, evitando que a análise se restrinja à acurácia geral.

A proposta é utilizar o Machine Learning como uma camada complementar de apoio à decisão de crédito, contribuindo para uma análise orientada por dados e para a investigação de padrões associados ao comportamento de pagamento. O modelo desenvolvido constitui uma prova de conceito e não deve ser interpretado como um sistema pronto para decisões reais de concessão de crédito, uma vez que seus resultados apresentam capacidade discriminativa limitada e exigem aprimoramentos e validações adicionais.

### Variável alvo

A variável-alvo (TARGET) foi construída a partir da variável STATUS, presente na base credit_record.csv, que registra o comportamento mensal de pagamento dos clientes.

Para transformar o problema em uma tarefa de classificação binária, os registros foram agrupados em duas categorias:

**0 – Bom pagador:** cliente que não apresentou registros classificados como atraso nos níveis considerados nesta análise;
**1 – Mau pagador:** cliente que apresentou pelo menos um registro com STATUS igual a 1, 2, 3, 4 ou 5.

Dessa forma, foram adotados os seguintes critérios de classificação:

**Bom pagador:** STATUS igual a 0, C ou X, desde que o cliente não apresente nenhum registro com status de 1 a 5;
**Mau pagador:** cliente que apresentou pelo menos um registro com STATUS igual a 1, 2, 3, 4 ou 5.

Os status de 1 a 5 representam diferentes níveis de atraso no histórico mensal de crédito. O status C indica crédito quitado, enquanto X representa ausência de informação de crédito naquele mês. Assim, esses dois últimos status, isoladamente, não caracterizam atraso segundo a regra adotada neste projeto.

A escolha de classificar como mau pagador qualquer cliente com pelo menos um registro de status entre 1 e 5 constitui uma regra operacional conservadora para a identificação de ocorrências de atraso. Ressalta-se, contudo, que essa definição representa o critério adotado para construir a variável-alvo, não uma classificação definitiva do comportamento financeiro do cliente.

Após a construção da variável-alvo por cliente, observou-se predominância da classe 0 em relação à classe 1, caracterizando o desbalanceamento das classes. Na base final utilizada na modelagem, aproximadamente **88,2% dos registros foram classificados como bons pagadores e 11,8% como maus pagadores.**

Esse desbalanceamento foi considerado durante a modelagem e a avaliação dos algoritmos. Por esse motivo, o desempenho não foi analisado exclusivamente pela acurácia, mas também por métricas como precisão (Precision), sensibilidade (Recall), F1-score, ROC-AUC, PR-AUC e acurácia balanceada (Balanced Accuracy).

**Observação:** A proporção de 88,2% e 11,8% refere-se à base final usada na modelagem, com 36.457 registros. A base target antes do cruzamento com os dados cadastrais, os percentuais são ligeiramente diferentes: aproximadamente 88,4% e 11,6%.

### Dataset

| Fonte | Kaggle – Credit Card Approval Prediction |

| URL | https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction |

| Arquivos | `application_record.csv` e `credit_record.csv` |

| Linhas × colunas – APPLICATION | 438.557 × 18 |

| Linhas × colunas – CREDIT | 1.048.575 × 3 |

| Período / versão | Dataset disponibilizado na plataforma Kaggle; não há período temporal/calendário explicitamente informado nos arquivos |

| Licença de uso | CC0: Domínio Público |

Descrição das variáveis:

#### `application_record.csv`

| Variável | Tipo | Descrição |
|---|---|---|
| `ID` | Inteiro | Identificador único do cliente. Utilizado para relacionar as bases. |
| `CODE_GENDER` | Categórica | Sexo informado do cliente. |
| `FLAG_OWN_CAR` | Categórica | Indica se o cliente possui automóvel. |
| `FLAG_OWN_REALTY` | Categórica | Indica se o cliente possui imóvel. |
| `CNT_CHILDREN` | Inteiro | Quantidade de filhos. |
| `AMT_INCOME_TOTAL` | Numérica | Renda anual informada pelo cliente. |
| `NAME_INCOME_TYPE` | Categórica | Tipo ou categoria de renda do cliente. |
| `NAME_EDUCATION_TYPE` | Categórica | Nível de escolaridade. |
| `NAME_FAMILY_STATUS` | Categórica | Estado civil ou situação familiar. |
| `NAME_HOUSING_TYPE` | Categórica | Tipo de moradia. |
| `DAYS_BIRTH` | Inteiro | Idade representada em dias, contada de forma relativa e negativa em relação à data de referência. |
| `DAYS_EMPLOYED` | Inteiro | Tempo relacionado ao vínculo empregatício, representado em dias de forma relativa. |
| `FLAG_MOBIL` | Binária | Indica se o cliente possui telefone celular. |
| `FLAG_WORK_PHONE` | Binária | Indica se o cliente possui telefone profissional. |
| `FLAG_PHONE` | Binária | Indica se o cliente possui telefone. |
| `FLAG_EMAIL` | Binária | Indica se o cliente possui endereço de e-mail. |
| `OCCUPATION_TYPE` | Categórica | Tipo de ocupação profissional do cliente. |
| `CNT_FAM_MEMBERS` | Numérica | Quantidade de integrantes da família. |

#### `credit_record.csv`

| Variável | Tipo | Descrição |
|---|---|---|
| `ID` | Inteiro | Identificador do cliente, utilizado para relacionar o histórico à base cadastral. |
| `MONTHS_BALANCE` | Inteiro | Índice relativo do mês do registro. O valor 0 representa o mês de referência e valores negativos representam meses anteriores. |
| `STATUS` | Categórica | Status mensal do comportamento de crédito do cliente. Os valores representam diferentes situações de pagamento e atraso. |

Obs.: A variável STATUS possui os códigos 0, 1, 2, 3, 4, 5, C e X; os valores de 1 a 5 representam níveis crescentes de atraso, C representa crédito quitado e X indica ausência de crédito/registro naquele mês.

---

## 4. Como reproduzir

```bash
git clone (https://github.com/lilianfo1983/tech-challenge-fase2-grupo28.git)>
cd <tech-challenge-fase2-grupo28>

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt
jupyter notebook
```

Baixe o dataset e coloque o arquivo bruto em `data/raw/` (os dados **não** são versionados —
veja `data/README.md`).

Depois execute os notebooks nesta ordem:

| # | Notebook | O que faz |

| 1 | `notebooks/Tech_Challenge_grupo28_v3.ipynb` | Análise exploratória, limpeza, escala, feature engineering, treina e compara os modelos, métricas, importância de variáveis e conclusão  |

**Semente fixa:** `RANDOM_STATE = 42`, declarada na primeira célula de cada notebook.
Rodar os notebooks na ordem acima, a partir de um ambiente limpo, deve reproduzir
exatamente os números da seção 5.

---

## 5. Resultados

| Modelo | Acurácia | Precisão | Recall | F1-score | AUC-ROC | PR-AUC | Acurácia balanceada |
|---|---:|---:|---:|---:|---:|---:|---:|
| Regressão Logística | 0.555 | 0.118 | 0.421 | 0.184 | 0.512 | 0.126 | 0.497 |
| Random Forest | 0.861 | 0.156 | 0.038 | 0.060 | 0.512 | 0.127 | 0.505 |
| Extra Trees | 0.813 | 0.135 | 0.105 | 0.118 | 0.507 | 0.125 | 0.507 |

**Modelo escolhido:** Regressão Logístic - Entre os três modelos avaliados, apresentou o maior Recall (0,421) e o maior F1-score (0,184). Entretanto, sua precisão foi baixa (0,118) e a AUC-ROC ficou próxima de 0,5, indicando capacidade discriminativa limitada. Portanto, foi escolhida como a alternativa mais promissora entre os modelos testados, mas ainda necessita de melhorias e validações antes de qualquer uso real na concessão de crédito..

**Métricas priorizadas:** Recall e F1-score, considerando o objetivo de identificar uma proporção maior de clientes classificados como maus pagadores. A precisão, a AUC-ROC, a PR-AUC e a acurácia balanceada também foram consideradas na avaliação comparativa dos modelos.

No contexto de análise de risco de crédito, o *Recall* é importante para medir a proporção de clientes classificados como maus pagadores que o modelo consegue identificar, ajudando a avaliar quantos casos de risco deixam de ser detectados. A *Precision*, por sua vez, indica a proporção de clientes previstos como maus pagadores que realmente pertencem a essa classe, permitindo avaliar a frequência de falsos positivos e o potencial de decisões excessivamente restritivas. O F1-score sintetiza o equilíbrio entre *Precision* e *Recall*, enquanto a AUC-ROC avalia a capacidade do modelo de distinguir as duas classes em diferentes limiares de classificação. A PR-AUC também é relevante neste projeto, pois a classe de maus pagadores é minoritária. Essas métricas devem ser analisadas em conjunto para orientar a comparação entre os modelos.

---

## 6. Principais Conclusoes


**1-** A identificação de maus pagadores é um desafio relevante. A base de modelagem apresenta aproximadamente 11,8% de clientes classificados como maus pagadores, evidenciando o desbalanceamento das classes. Por isso, a avaliação dos modelos considerou métricas além da acurácia, priorizando a capacidade de identificar casos associados ao risco de atraso.

**2-** A Regressão Logística apresentou o melhor resultado para a identificação de maus pagadores entre os modelos testados. O modelo alcançou Recall de 0,421 e F1-score de 0,184, superando Random Forest e Extra Trees nessas métricas. Entretanto, sua precisão de 0,118 indica elevada ocorrência de falsos positivos, o que pode levar à classificação indevida de bons pagadores como clientes de risco.

**3**- As variáveis cadastrais e profissionais contribuíram de forma diferente para as previsões. Na análise de importância por permutação da Regressão Logística, destacaram-se OCCUPATION_TYPE (tipo de ocupação), EMPLOYED_YEARS (tempo de emprego), NAME_EDUCATION_TYPE (escolaridade) e FLAG_OWN_CAR (posse de automóvel). Essas variáveis apresentaram maior contribuição relativa para o desempenho preditivo observado, mas não demonstram, por si só, relações causais com a inadimplência.

**4-** Os resultados ainda não demonstram capacidade suficiente para uso operacional. Os valores de AUC-ROC ficaram próximos de 0,5 nos três modelos, indicando capacidade limitada de discriminação entre bons e maus pagadores. Portanto, os resultados devem ser interpretados como uma prova de conceito, e não como evidência de que o modelo já seja adequado para decidir concessões de crédito.

**5-** Há oportunidades de aprimoramento antes de uma aplicação prática. Recomenda-se investigar novas variáveis, revisar a definição da variável-alvo, avaliar diferentes estratégias de tratamento do desbalanceamento e testar ajustes dos modelos e dos limiares de classificação. Também são necessárias validações adicionais para avaliar a estabilidade dos resultados e os impactos dos falsos positivos e falsos negativos no processo de concessão de crédito.

### Limitações e próximos passos

O modelo foi desenvolvido com base em dados históricos e seu desempenho pode variar quando aplicado a novos perfis de clientes ou em cenários econômicos diferentes. Além disso, a variável-alvo foi construída a partir dos registros mensais de status de crédito disponíveis na base, considerando como maus pagadores os clientes que apresentaram pelo menos uma ocorrência de atraso classificada entre os status de 1 a 5. Essa definição constitui uma regra operacional para o projeto e não representa necessariamente todas as dimensões consideradas em uma decisão real de concessão de crédito.

Os resultados obtidos também evidenciaram limitações na capacidade de discriminação dos modelos avaliados, cujos valores de AUC-ROC ficaram próximos de 0,5. Embora a Regressão Logística tenha apresentado o maior Recall e F1-score entre os algoritmos testados, sua precisão foi baixa, indicando uma elevada ocorrência de falsos positivos. Dessa forma, o modelo ainda não apresenta desempenho suficiente para ser utilizado isoladamente em decisões reais de concessão de crédito.

Como próximos passos, recomenda-se realizar validação cruzada, testar diferentes hiperparâmetros, investigar novas variáveis preditivas e avaliar estratégias de tratamento do desbalanceamento das classes. Também é importante analisar diferentes pontos de corte das probabilidades e avaliar seus impactos sobre falsos positivos e falsos negativos. A calibração das probabilidades, a estabilidade temporal e a capacidade de generalização do modelo devem ser investigadas em avaliações adicionais.

Em uma aplicação real, também devem ser considerados aspectos de governança, explicabilidade, privacidade e possíveis vieses relacionados às variáveis utilizadas, especialmente aquelas associadas a características pessoais dos clientes. Antes de qualquer implantação, seria necessária uma validação independente, acompanhada de monitoramento contínuo do desempenho e dos impactos das previsões no processo de concessão de crédito.

---

## 7. Estrutura do repositorio

```
├── .gitignore
├── CHECKLIST.md
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
│   ├── Tech_Challenge_grupo28_v3.ipynb
│   └── README.md
│
└── results/
    ├── figures/                       Gráficos da análise e avaliação
    ├── metrics/                       Métricas, previsões e importância das variáveis
    └── models/
        └── modelo_logistic_regression.joblib
```
As bases de dados originais e os dados processados não são versionados no GitHub. As instruções para obtenção dos dados estão disponíveis em data/README.md.

A pasta results/figures reúne os gráficos gerados durante a análise exploratória e a avaliação dos modelos. A pasta results/metrics contém os arquivos CSV com as métricas de desempenho, as previsões da Random Forest e a importância das variáveis da Regressão Logística. Já a pasta results/models armazena o modelo treinado de Regressão Logística, salvo no formato Joblib.

```

Detalhes e convenções em [`ESTRUTURA.md`](ESTRUTURA.md).
Antes de enviar, percorra o [`CHECKLIST.md`](CHECKLIST.md).

---

## 8. Tecnologias

```

**Python 3.11 — ** linguagem de programação utilizada no projeto
**Pandas —** manipulação e análise dos dados
**NumPy —** operações numéricas
**Scikit-learn —**pré-processamento, construção de pipelines, treinamento e avaliação dos modelos
**Matplotlib —** criação de gráficos e visualizações
**Seaborn —** visualização de dados e análise exploratória
**Jupyter Notebook —** desenvolvimento, execução e documentação das análises
**Joblib —** serialização e armazenamento do modelo treinado
**Git e GitHub —** versionamento e compartilhamento do projeto
