# ModeloRendaLinear
## 1. Ajuste um modelo para prever log(renda) considerando todas as covariáveis disponíveis.

1.1. Utilizando os recursos do Patsy, coloque as variáveis qualitativas como dummies.

1.1.1. Importe as bibliotecas necessárias (pandas, statsmodels, patsy, numpy).

1.1.2. Carregue os dados do arquivo 'previsao_de_renda.csv' usando o pandas.

1.1.3. Identifique variáveis categóricas e crie uma fórmula Patsy com dummies.

1.1.4. Crie as matrizes de design e ajuste o modelo de regressão múltipla.

1.1.5. Avalie os parâmetros e veja se parecem fazer sentido prático.

python ```

import pandas as pd
import statsmodels.api as sm
import patsy
import numpy as np

Carregar os dados
df = pd.read_csv('previsao_de_renda.csv')

Identificar variáveis categóricas
categorical_columns = df.select_dtypes(include=['object']).columns

Criar a fórmula com o Patsy, incluindo variáveis qualitativas como dummies
formula = 'np.log(renda) ~ ' + ' + '.join(['C({0}, Treatment(reference="{1}"))'.format(column, df[column].mode().iloc[0]) for column in categorical_columns.difference(['renda'])])

Criar as matrizes de design usando patsy
y, X = patsy.dmatrices(formula, df, return_type='dataframe')

Ajustar o modelo de regressão múltipla
model = sm.OLS(y, X)
result = model.fit()

Imprimir os resultados
print(result.summary())
```


