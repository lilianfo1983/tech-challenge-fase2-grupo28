# data/

**Nada aqui é versionado.** O `.gitignore` bloqueia o conteúdo destas pastas de propósito:
datasets em Git incham o repositório e frequentemente violam a licença da fonte.

| Pasta | Conteúdo |
|---|---|
| `raw/` | arquivo original, exatamente como baixado da fonte — nunca editado |
| `processed/` | saída dos notebooks de pré-processamento (`.parquet` ou `.csv`) |

Documente abaixo como obter os dados brutos, para que qualquer pessoa consiga reproduzir o projeto.

### application_record.csv

- Baixe em: [Kaggle](https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction)
- Arquivo: `application_record.csv`
- Local: `data/raw/application_record.csv`
- SHA-256: '4833F502D02AD94295DE3FFE74F665E726A4B04342D2E94F8CEC41DCE951925B'

### credit_record.csv

- Fonte: [Kaggle](https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction)
- Arquivo: `credit_record.csv`
- Local: `data/raw/credit_record.csv`
- SHA-256: 'BA0006A4734F74422D68B0A7132AD591850BE0A6AFFB535EB1042D207FE4B27E'