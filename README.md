# mvp-comercio-exterior
Análise de exportações brasileiras de 1996 a 2023 com base em dados do Kaggle.

# 📊 Análise de Exportações Brasileiras (ComexStat)

Este notebook faz parte do projeto MVP da Pós-graduação em Ciência de Dados e Analytics. O objetivo é analisar dados de exportações brasileiras, utilizando informações públicas da plataforma ComexStat, com foco em produtos exportados, países de destino e valor FOB.

---

## 📌 Índice

1. [Objetivo do Projeto](#objetivo-do-projeto)
2. [Fonte dos Dados](#fonte-dos-dados)
3. [Tratamento e Preparação dos Dados](#tratamento-e-prepara%C3%A7%C3%A3o-dos-dados)
4. [Análise de Produtos Exportados](#an%C3%A1lise-de-produtos-exportados)
5. [Análise por País de Destino](#an%C3%A1lise-por-pa%C3%ADs-de-destino)
6. [Visualizações](#visualiza%C3%A7%C3%B5es)
7. [Modelagem DW Simulada](#modelagem-dw-simulada)
8. [Conclusão](#conclus%C3%A3o)



## 🔍 Objetivos

- Identificar os principais produtos exportados pelo Brasil
- Analisar os principais países compradores
- Observar padrões e tendências ao longo do tempo
- Criar visualizações para facilitar a interpretação dos dados

## 📁 Fonte dos Dados

Os dados utilizados neste projeto foram obtidos a partir do ComexStat (https://comexstat.mdic.gov.br/pt/comex-vis), portal oficial do governo brasileiro.

## 🧠 Ferramentas Utilizadas

- Python
- Pandas
- Seaborn
- Matplotlib
- Google Colab

## 📊 Análises Realizadas

- Cálculo dos produtos mais exportados por valor FOB (Free on Board)
- Agrupamento por país de destino das exportações
- Visualizações em gráfico de barras e linha para facilitar a análise

## 📈 Resultados

As análises permitiram observar que determinados produtos, como commodities agrícolas e minerais, representam a maior parte das exportações brasileiras. A China, os Estados Unidos e a Argentina figuram entre os principais destinos das exportações nacionais.

## 🚀 Como Executar

1. Acesse o [Google Colab](https://colab.research.google.com/)
2. Faça upload do notebook `MVP_Dados_Comércio_Exterior.ipynb`
3. Execute célula por célula
4. Certifique-se de que o arquivo CSV esteja disponível ou já carregado

## 🧱 Modelagem DW Simulada (Data Warehouse)

Como parte do aprendizado em Banco de Dados, Data Warehouse e Governança, este projeto também simula como os dados analisados poderiam ser organizados em um modelo dimensional do tipo **Esquema Estrela**, compatível com ferramentas como Google BigQuery.

### 🔹 Tabela fato: `fato_exportacoes`
Contém os dados quantitativos que serão analisados.

| Coluna           | Tipo   | Descrição                                  |
|------------------|--------|---------------------------------------------|
| id_exportacao    | INT    | Identificador único (pode ser auto gerado) |
| id_tempo         | INT    | Chave para a dimensão tempo                |
| id_produto       | INT    | Chave para a dimensão produto              |
| id_pais          | INT    | Chave para a dimensão país                 |
| valor_fob        | FLOAT  | Valor FOB (US$)                            |
| kg_liquido       | FLOAT  | Peso líquido exportado                     |

---

### 🔹 Dimensão Tempo: `dim_tempo`

| Coluna    | Tipo  | Descrição        |
|-----------|-------|------------------|
| id_tempo  | INT   | Chave primária   |
| ano       | INT   | Ano da exportação|
| mes       | INT   | Mês da exportação|

---

### 🔹 Dimensão Produto: `dim_produto`

| Coluna      | Tipo   | Descrição                         |
|-------------|--------|-----------------------------------|
| id_produto  | INT    | Código NCM                        |
| nome_produto| STRING | Nome do produto (se disponível)  |

---

### 🔹 Dimensão País: `dim_pais`

| Coluna     | Tipo   | Descrição              |
|------------|--------|------------------------|
| id_pais    | INT    | Código do país         |
| nome_pais  | STRING | Nome do país           |

---

### ☁️ Carga no BigQuery (simulada)

Caso fosse necessário subir os dados para o BigQuery, a carga poderia ser feita com o seguinte fluxo:

- **Extração:** dados públicos do ComexStat em `.csv`
- **Transformação:** limpeza e agrupamento com Pandas
- **Carga:** upload para o BigQuery via `pandas_gbq.to_gbq()` ou scripts SQL

Exemplo em Python:
```python
from pandas_gbq import to_gbq

to_gbq(df_export,
       destination_table='mvp_dw.fato_exportacoes',
       project_id='seu-projeto-gcp',
       if_exists='replace')


## Conclusão

Através da análise dos dados de exportação do Brasil, foi possível identificar que produtos como carnes e soja estão entre os mais exportados, e países como China e EUA estão entre os principais compradores.

Essas informações podem ser usadas para orientar estratégias comerciais e entender o comportamento do mercado externo brasileiro.


## 👩‍💻 Autora

Danielly Pereira de Arruda

---

