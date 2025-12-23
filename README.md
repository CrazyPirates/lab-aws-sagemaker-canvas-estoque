# 🏠 Previsão de Aluguel de Casas na AWS com [SageMaker Canvas](https://aws.amazon.com/pt/sagemaker/canvas/)

Este projeto foi desenvolvido como parte de um desafio prático da **DIO (Digital Innovation One)**, utilizando o **Amazon SageMaker Canvas** para criar um modelo de Machine Learning *No-Code*.

O objetivo foi prever o valor do aluguel (`rent`) com base em características de imóveis na Índia.

## 📋 Passo a Passo do Projeto

### 1. Seleção do Dataset

O dataset utilizado foi o `India House Rent Prediction`, carregado via upload local e pego no Kaggle. Este conjunto de dados contém informações sobre imóveis, como localização, número de quartos, banheiros, tamanho, etc.

![Upload do Dataset](/images/1.PNG)

### 2. Construção e Treinamento (Build & Train)

No SageMaker Canvas, o dataset foi importado e configurado para o treinamento.
- **Target:** `rent` (Valor do aluguel).
- **Configurações do Modelo:**
    - Remoção de colunas irrelevantes e para evitar vazamento de dados (`house_type`, `area_rate`).
    - Limpeza de dados: Remoção de linhas com `area` menor que 100 e remoção de duplicatas.
    - O modelo utilizou uma estratégia de *Quick Build* para gerar previsões iniciais.

![Configuração do Modelo](/images/2.PNG)

### 3. Análise de Métricas (Analyze)

Após o treinamento, o modelo alcançou as seguintes métricas de performance:

- **RMSE (Root Mean Square Error):** 46671.828 (Margem média de erro).
- **R² (Coeficiente de Determinação):** 72.282% (O modelo explica cerca de 72% da variabilidade dos preços).

![Status do Modelo](/images/3.PNG)
![Métricas Avançadas](/images/5.PNG)

#### Gráfico de Previsão vs. Real
Abaixo, podemos visualizar a dispersão entre os valores reais e os previstos. A linha central representa a previsão ideal.

![Previsão vs Real](/images/4.PNG)

#### Impacto das Colunas (Feature Importance)
O SageMaker identificou quais características mais influenciam o preço do aluguel. As variáveis mais importantes foram:

![Impacto das Colunas](/images/6.PNG)

### 4. Previsão (Predict)

Com o modelo treinado, foi realizado um teste de previsão ("Single Prediction") para validar o funcionamento. O modelo estimou um aluguel de **43.901,16** para o cenário testado.

![Resultado da Previsão](/images/single_prediction_results.png)

## 🚀 Conclusões e Insights

1. **Fatores Determinantes:** O tamanho do imóvel (`area`) e a quantidade de banheiros (`bathrooms`) são os fatores mais decisivos para o valor do aluguel, somando quase 60% da influência no preço.
2. **Performance:** O modelo obteve um **R² de 72%**, o que é um resultado sólido para um primeiro ciclo de treinamento, indicando que ele consegue generalizar bem a maioria dos casos.
3. **Oportunidades de Melhoria:** O RMSE de 46k sugere que ainda há uma margem de erro considerável para imóveis de valores muito altos ou atípicos. Um Standard Build ou mais feature engineering poderiam refinar essa precisão.
