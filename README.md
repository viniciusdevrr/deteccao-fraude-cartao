# Detecção de fraude em cartões de crédito

Notebook em Python para detecção de transações fraudulentas com classes desbalanceadas. A base contém aproximadamente 0,17% de fraudes; por isso, acurácia isolada pode ser enganosa. O foco é o **recall da classe fraude**, acompanhado de precisão, F1, ROC AUC e Average Precision.

## Como executar

1. Abra [`deteccao_fraude.ipynb`](deteccao_fraude.ipynb) no Google Colab.
2. Selecione **Ambiente de execução → Executar tudo**.
3. Aguarde o download da base pública e o treinamento; salve o notebook com as saídas antes de enviar.

Fonte dos dados: [Kaggle — Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud). O `creditcard.csv` é baixado em tempo de execução via `kagglehub` e **não está no repositório**. Se o download exigir autenticação, faça login no Kaggle no ambiente de execução.

## Preparação e modelos

Criação de `log_amount`, divisão estratificada de treino/teste e validação separada; padronização dentro do pipeline da regressão logística para evitar vazamento. Comparação entre regressão logística, Random Forest e XGBoost, usando ponderação das classes. O teste mantém a distribuição original.

## Métricas e limiar

O limiar de cada modelo é escolhido pela maximização de **F2 na validação**, privilegiando recall, e depois avaliado no teste. A tabela final do notebook apresenta precisão, recall, F1 da classe fraude, ROC AUC e Average Precision; também inclui matrizes de confusão e curvas ROC e precisão-recall. **Preencha abaixo somente depois de executar o notebook:**

| Modelo | Limiar | Precisão fraude | Recall fraude | F1 fraude |
|---|---:|---:|---:|---:|
| Regressão Logística | 0.9996	| 0.6457	 | 0.8367 | 0.7289	 |
| Random Forest | 	0.2074	 | 0.6418 | 0.8776 | 0.7414 |
| XGBoost | 0.8561	 | 0.7830 | 0.8469 | 0.8137 |

## Explicabilidade e diferenças do roteiro

A importância das variáveis e os gráficos SHAP do XGBoost mostram quais componentes influenciaram as previsões. Como `V1`–`V28` são componentes PCA anonimizados, não se atribui a eles um significado de negócio específico. Em relação ao roteiro proposto, o projeto adiciona validação independente para seleção do limiar via F2 e a transformação `log_amount`. Após executar, descreva aqui 1–2 variáveis que mais apareceram nos gráficos SHAP e a direção da contribuição observada, sem inferir causalidade.
