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
| Vídeo executivo (≤ 5 min) | <[!-- PREENCHER: YouTube não listado / Drive com acesso liberado --](https://youtu.be/NZP1FulhNuY)> |
| Apresentação | <(https://github.com/michelleventura56-a11y/Tech---Challenge---fase-2---Grupo-28/blob/main/docs/Apresentacao%20Risco%20Cr%C3%A9dito%20-Tech%20Chalange%20Grupo28.pdf)> |

> ⚠️ Repositório privado ou inacessível inviabiliza a avaliação da entrega.
> Confira o acesso em uma janela anônima antes de enviar.

---

## 3. O problema

## 3. O problema

A concessão de crédito é uma atividade estratégica para instituições financeiras, pois permite ampliar o relacionamento com clientes e gerar receitas, mas também envolve o risco de inadimplência.
A análise tradicional de crédito pode envolver grande quantidade de informações cadastrais, financeiras e comportamentais, tornando relevante a utilização de técnicas de análise de dados e Machine Learning para identificar padrões associados ao risco de pagamento.
Neste projeto, o problema é tratado como uma tarefa de classificação supervisionada, cujo objetivo é identificar clientes com maior probabilidade de apresentar comportamento associado à inadimplência.
A solução proposta utiliza informações cadastrais, pessoais, profissionais e financeiras dos clientes, combinadas com seu histórico de crédito. Diferentes algoritmos de classificação são treinados e comparados para identificar aquele que apresenta melhor capacidade de discriminação entre bons e maus pagadores.
A utilização de Machine Learning pode contribuir como uma camada adicional de apoio à decisão de crédito, permitindo tornar a análise mais consistente, escalável e orientada por dados.
É importante destacar que o modelo desenvolvido neste projeto representa uma prova de conceito e ferramenta de apoio à decisão, não devendo ser interpretado como substituto automático das políticas de concessão de crédito de uma instituição financeira.

### Variável alvo

A variável alvo (`target`) foi construída a partir da variável `STATUS`, presente na base `credit_record.csv`, que registra o comportamento mensal de pagamento dos clientes.
Para transformar o problema em uma classificação binária, os registros foram agrupados em duas categorias:
- **0 – Bom pagador:** cliente que não apresentou registros classificados como inadimplência no histórico considerado;
- **1 – Mau pagador:** cliente que apresentou pelo menos um registro com `STATUS` igual a 1, 2, 3, 4 ou 5.

Assim, foi adotado como critério de classificação o seguinte conjunto de status:

**Bom pagador:** `0`, `C` ou `X`  
**Mau pagador:** `1`, `2`, `3`, `4` ou `5`

Os status de `1` a `5` representam diferentes níveis de atraso, enquanto `C` representa uma situação de crédito quitada e `X` indica ausência de informação de crédito naquele mês. A documentação disponível sobre a base confirma a utilização desses códigos para representar o comportamento mensal de crédito. 

A escolha de considerar como mau pagador qualquer cliente que tenha apresentado pelo menos um registro entre `1` e `5` foi adotada como uma regra conservadora de risco, pois permite identificar clientes que apresentaram algum nível de atraso em seu histórico.

Após a construção da variável alvo, observou-se uma predominância da classe 0 (bons pagadores) em relação à classe 1 (maus pagadores), caracterizando um problema de desbalanceamento de classes.

Esse desbalanceamento foi considerado durante a modelagem e avaliação. Por esse motivo, o desempenho dos modelos não foi avaliado somente pela acurácia, sendo utilizadas métricas como Precision, Recall, F1-score, ROC-AUC e PR-AUC.

### Dataset

| Campo | Valor |
|---|---|
| Fonte | <!-- PREENCHER: URL --> |
| Linhas × colunas | <!-- PREENCHER --> |
| Período / versão | <!-- PREENCHER --> |
| Licença de uso | <!-- PREENCHER --> |

| Fonte | Kaggle – Credit Card Approval Prediction |
| URL | https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction
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

| Modelo | Acurácia | Precisão | Recall | F1 | AUC-ROC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Regressão Logística | 0.577 | 0.137 | 0.491 | 0.215 | 0.549 | 0.142 |
| Random Forest | 0.841 | 0.373 | 0.515 | 0.433 | 0.780 | 0.375 |
| Extra Trees | 0.794 | 0.309 | 0.606 | 0.409 | 0.770 |0.368 |

**Modelo escolhido:** Random Forest — apresentou o melhor desempenho geral entre os modelos avaliados, com o maior AUC-ROC (0.780), maior F1-score (0.433) e maior precisão (0.373). Embora o Extra Trees tenha apresentado maior Recall (0.606), o Random Forest apresentou um equilíbrio mais adequado entre capacidade de identificação dos maus pagadores e controle de falsos positivos.

**Métricas priorizadas:** Foram priorizadas Precision, Recall, F1-score e AUC-ROC, complementadas pela análise de PR-AUC e Balanced Accuracy. A escolha considera o desbalanceamento das classes, uma vez que aproximadamente 88,2% dos clientes pertencem à classe de bons pagadores e 11,7% à classe de maus pagadores. Nesse contexto, a acurácia isoladamente poderia fornecer uma percepção inadequada do desempenho do modelo.

No contexto de crédito, o Recall é importante para medir a capacidade de identificar clientes classificados como maus pagadores, reduzindo o risco de conceder crédito a clientes com maior probabilidade de inadimplência. A Precision, por sua vez, permite avaliar quantos dos clientes classificados como maus pagadores realmente pertencem a essa classe, ajudando a controlar decisões excessivamente restritivas. O F1-score foi utilizado para avaliar o equilíbrio entre Precision e Recall, enquanto o AUC-ROC mede a capacidade geral de discriminação entre as classes.

---

## 6. Principais conclusões

<!-- PREENCHER: 3 a 5 conclusões em linguagem de negócio.
     Inclua quais variáveis mais influenciam o resultado e o que isso significa
     na prática para quem vai usar o modelo. -->

1. O modelo Random Forest apresentou o melhor desempenho geral entre os algoritmos avaliados, alcançando AUC-ROC de 0.780 e F1-score de 0.433. O resultado indica uma capacidade relevante de diferenciar clientes com maior e menor risco de inadimplência.

2. O modelo identificou aproximadamente 51,5% dos maus pagadores no conjunto de teste (Recall = 0.515). Esse resultado demonstra potencial para apoiar a triagem de propostas e direcionar análises mais detalhadas para clientes com maior risco.

3. As variáveis com maior importância preditiva foram idade, posse de imóvel, tipo de ocupação, tipo de renda e tempo de emprego. Na prática, essas características apresentam maior contribuição para a capacidade preditiva do modelo e podem auxiliar na compreensão dos padrões associados ao risco de crédito.

5. O conjunto de dados apresenta desbalanceamento entre bons e maus pagadores. Por isso, a utilização de métricas como Recall, Precision, F1-score, AUC-ROC e PR-AUC é mais adequada do que avaliar o modelo somente pela acurácia.

6. O modelo deve ser utilizado como ferramenta de apoio à decisão, e não como substituto integral da análise de crédito. Sua utilização pode contribuir para tornar a análise mais consistente, priorizar casos de maior risco e apoiar decisões baseadas em evidências históricas.

### Limitações e próximos passos

O modelo foi desenvolvido com base em dados históricos e, portanto, seu desempenho pode sofrer alterações quando aplicado a novos perfis de clientes ou em cenários econômicos diferentes. Além disso, a definição da variável-alvo foi baseada no histórico de status de crédito disponível na base, não representando necessariamente todas as dimensões utilizadas em uma decisão real de concessão de crédito.

Como próximos passos, recomenda-se realizar validação cruzada, testar diferentes hiperparâmetros e estratégias de definição do ponto de corte das probabilidades. Também é importante avaliar a calibração das probabilidades, acompanhar a estabilidade do modelo ao longo do tempo e monitorar possíveis mudanças no perfil dos clientes.

Em uma aplicação real, também devem ser avaliados aspectos de governança, explicabilidade e possíveis vieses relacionados às variáveis utilizadas, especialmente aquelas que possam estar associadas a características pessoais dos clientes.

---

## 7. Estrutura do repositório

```
.
├── data/          dados brutos (raw) e tratados (processed) — não versionados
├── notebooks/     análise em ordem numerada
└── docs/          apresentação executiva
```

Detalhes e convenções em [`ESTRUTURA.md`](ESTRUTURA.md).
Antes de enviar, percorra o [`CHECKLIST.md`](CHECKLIST.md).

---

## 8. Tecnologias

- **Python 3.11**
- **Pandas** — manipulação e análise dos dados
- **NumPy** — operações numéricas
- **Scikit-learn** — pré-processamento, pipelines, treinamento e avaliação dos modelos
- **Matplotlib** — visualização de dados
- **Seaborn** — visualização e análise exploratória
- **Jupyter Notebook** — desenvolvimento e documentação das análises
- **Git e GitHub** — versionamento e compartilhamento do projeto
