# Projeto de Análise de Dados: Previsão da Execução Orçamentária do MEC

## 1. Contexto do Problema

Este projeto explora os dados de execução orçamentária do Ministério da Educação (MEC) para desenvolver um modelo de Machine Learning capaz de prever a probabilidade de uma dotação orçamentária ser executada com sucesso. A execução eficiente do orçamento público é um desafio constante, e a análise preditiva pode ser uma ferramenta valiosa para gestores identificarem gargalos e atuarem de forma proativa.

O objetivo é classificar a execução em três categorias: **Baixa**, **Média** e **Alta**.

## 2. O Desafio Inicial: Um Modelo Estagnado

O desenvolvimento inicial do modelo, utilizando um algoritmo `RandomForestClassifier` com as features mais óbvias (Órgão, Ação, Grupo de Despesa), resultou em uma performance modesta e estagnada em aproximadamente **58% de acurácia**.

Diversas abordagens iniciais, como o tratamento de classes desbalanceadas (`class_weight='balanced'`) e o agrupamento de categorias raras, não surtiram o efeito esperado. Isso levou à hipótese de que o problema não residia no algoritmo, mas na falta de features com real poder preditivo.

<img width="476" height="199" alt="image" src="https://github.com/user-attachments/assets/c47fc3cc-ddd7-4f5c-bb96-010808612159" />

## 3. Metodologia e Engenharia de Features: O Ponto da Virada

A estratégia foi pivotada para uma profunda **Engenharia de Features**, buscando enriquecer o dataset com mais contexto. As seguintes etapas foram cruciais:

* **Inclusão de Novas Variáveis Categóricas:** Foram adicionadas ao modelo colunas como `NOME CATEGORIA ECONÔMICA`, `NOME PROGRAMA ORÇAMENTÁRIO` e `NOME SUBFUNÇÃO`, que descrevem a natureza do gasto com mais detalhes.
* **Criação de Features Relacionais:** Foi criada a feature `PROPORCAO_NO_ORGAO`, que calcula o peso de uma dotação orçamentária em relação ao orçamento total do seu órgão.
* **Otimização de Hiperparâmetros:** Após a melhoria das features, foi utilizado o `RandomizedSearchCV` para realizar um ajuste fino nos parâmetros do RandomForest, buscando o máximo de performance.

## 4. Resultados e Análise

A combinação de uma engenharia de features robusta com a otimização de hiperparâmetros elevou a acurácia do modelo para **61.06%**.

Mais importante que o aumento da acurácia geral, foi a melhora significativa na capacidade do modelo de identificar as classes minoritárias ('Alta' e 'Média'), como pode ser visto no `recall` do relatório de classificação e na Matriz de Confusão final.

#### Relatório de Classificação Final

<img width="476" height="199" alt="image" src="https://github.com/user-attachments/assets/008312d2-0cb3-44ab-884c-eb4c22a4b89f" />

#### Matriz de Confusão Final

<img width="552" height="436" alt="image" src="https://github.com/user-attachments/assets/99bd5a6e-dbe8-4e81-9d9c-ef6f93d59f22" />

O modelo final é mais equilibrado e inteligente, demonstrando que o enriquecimento dos dados foi a chave para o sucesso.

## 5. Conclusões e Próximos Passos

Este projeto reforça uma lição fundamental em Ciência de Dados: a qualidade e o contexto das features frequentemente superam a complexidade do algoritmo. Embora uma acurácia de 61% indique que o problema é inerentemente complexo, a jornada de diagnóstico e solução de problemas demonstrou a aplicação de um processo metodológico robusto.

Como próximos passos para evoluir o projeto, recomenda-se:
* **Inclusão de Dados Históricos:** A adição de dados de anos anteriores para criar features de tendência e performance passada.
* **Experimentação com outros Algoritmos:** Testar modelos como XGBoost e LightGBM, que podem oferecer performance superior.

## 6. Como Rodar o Projeto

1. Clone o repositório.
2. Crie um ambiente virtual (`python -m venv venv`).
3. Instale as dependências: `pip install -r requirements.txt`.
4. Abra o Jupyter Notebook `analise_orcamentaria_mec.ipynb` e execute as células.

5. O dataset pode ser baixado no Portal da Transparência do Governo Federal.
