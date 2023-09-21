# Documentação do Modelo Preditivo do Índice da Ibovespa

Este documento descreve um modelo preditivo para prever o preço das ações do Ibovespa com base em dados históricos. O modelo utiliza técnicas de regressão com diferentes algoritmos e avalia o desempenho de cada modelo. O código foi desenvolvido em Python com o uso de bibliotecas como pandas, numpy, scikit-learn e matplotlib.

## 1. Entendendo o Dataset de Entrada

O dataset de entrada contém informações históricas sobre o índice da Ibovespa. Ele inclui os seguintes atributos:

- Data
- Último (Preço de Fechamento)
- Abertura
- Máxima
- Mínima
- Volume (Vol.)
- Variação Percentual (Var%)

## 2. Ajustando os Dados

Nesta seção, os dados foram processados para torná-los adequados para treinar e testar modelos de machine learning. Isso incluiu as seguintes etapas:

- Limpeza da coluna "Vol." para remover caracteres não numéricos, como "K" e "M", e converter para valores numéricos.
- Limpeza da coluna "Var%" para remover o símbolo "%" e substituir vírgulas por pontos, convertendo-a em valores numéricos.
- Transformação da coluna "Data" em formato de data para melhor manipulação.
- Ordenar por "Data".
- Definir a coluna "Data" como índice.
- Cálculo das médias móveis de 30 dias (MM30) para "Vol." e 360 dias (MM360) para "Último".
- Remoção de linhas com valores ausentes.

## 3. Definindo os Conjuntos de Treinamento e Teste

Os dados foram divididos em conjuntos de treinamento (70%) e teste (30%) para avaliar o desempenho dos modelos. A escala dos atributos foi normalizada usando o MinMaxScaler.

## 4. Definindo os Modelos

Foram treinados cinco modelos de regressão diferentes:

- Regressão Linear (`model_lr`)
- Árvore de Decisão (`model_dt`)
- Random Forest (`model_rf`)
- Regressão Ridge (`model_rd`)
- Gradient Boosting (`model_gb`)

Cada modelo foi treinado com os dados de treinamento normalizados.

## 5. Avaliando os Modelos

Os modelos foram avaliados com base em três métricas de desempenho:

- Mean Absolute Error (MAE): Média do valor absoluto das diferenças entre os valores reais e as previsões.
- Mean Squared Error (MSE): Média dos quadrados das diferenças entre os valores reais e as previsões.
- R-squared (R²): Uma medida de quão bem as variáveis independentes explicam a variabilidade da variável dependente.

Os resultados de desempenho foram apresentados para cada modelo, juntamente com gráficos que mostram a comparação entre os valores reais e as previsões.

## 6. Comparando os Modelos

Os modelos foram comparados com base nas métricas de desempenho MAE, MSE e R-squared. O objetivo é selecionar o modelo que oferece o melhor desempenho na previsão do preço das ações do Ibovespa.

## 7. Exportando os Modelos Treinados

Os modelos treinados foram exportados usando a biblioteca `joblib` e salvos em arquivos `.pkl` para uso futuro. Os modelos podem ser carregados novamente usando `joblib.load()` quando necessário.

Exemplo de exportação:
```python
import joblib

# Salvar os modelos usando joblib
joblib.dump(model_lr, 'models/LinearRegressionModel.pkl')
joblib.dump(model_dt, 'models/DecisionTreeModel.pkl')
joblib.dump(model_gb, 'models/GradientBoostingModel.pkl')
joblib.dump(model_rf, 'models/RandomForestModel.pkl')
joblib.dump(model_rd, 'models/RidgeModel.pkl')
```