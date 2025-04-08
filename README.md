# MVP - Engenharia de Dados | Pós PUC-Rio

Este projeto foi desenvolvido como parte da disciplina de MVP do curso de Pós-Graduação em Ciência de Dados e Analytics da PUC-Rio. 
O objetivo foi construir um pipeline de dados completo, utilizando a arquitetura de camadas Bronze, Silver e Gold, com análises feitas na plataforma Databricks.

## Fonte dos Dados

Utilizamos os dados públicos da empresa Olist, disponíveis em arquivos CSV, no Kaggle, que representam pedidos de e-commerce no Brasil. Os arquivos foram carregados no Databricks e armazenados em camadas de persistência.

## Objetivo

Investigar os principais fatores que influenciam a satisfação dos clientes no e-commerce brasileiro, com base nas avaliações de pedidos da Olist.

### Perguntas de negócio
1. Qual o perfil dos pedidos com melhores e piores avaliações?
2. O tempo de entrega impacta na nota da avaliação?
3. Há categorias de produtos com maiores taxas de insatisfação?
4. Compras com valor mais alto tendem a ter melhores avaliações?
5. Existem estados ou regiões com mais reclamações?
6. A forma de pagamento influencia a nota dada pelo cliente?

## Arquitetura do Pipeline

O projeto foi implementado com a arquitetura Medallion, estruturada em:

### Camada Bronze

Leitura e armazenamento dos dados brutos em formato Delta.
Nenhuma transformação aplicada, apenas padronização de formatos e tipos.

### Camada Silver

Tratamento de dados nulos e tipos incorretos.
Junção de tabelas relacionadas (ex: pedidos + produtos + avaliações).
Criação de colunas derivadas como delivery_days e tradução de categorias.

### Camada Gold

Modelagem analítica dos dados para responder às perguntas de negócio.
Criação de tabelas com agregados, filtros e colunas interpretativas.
Todas as tabelas Gold foram salvas com saveAsTable() e estão acessíveis via SQL no Databricks.

## Tecnologias Utilizadas

Databricks Community Edition (armazenamento, notebooks, execução de código)
PySpark (transformação e leitura de dados)
SQL (consultas e análise de negócio)
Formato Delta Lake (armazenamento de tabelas com versionamento)

## Principais Conclusões

Clientes insatisfeitos estão concentrados nas categorias mais populares, mas algumas menos conhecidas têm taxa de reclamação proporcional muito alta.
Tempo de entrega é o fator com maior correlação negativa com a nota de avaliação.
Pedidos de maior valor tendem a receber notas mais baixas.
Regiões Norte e Nordeste, além do RJ, apresentaram as maiores taxas proporcionais de insatisfação.
Forma de pagamento não influencia significativamente na satisfação do cliente.

## Estrutura de Diretórios (GitHub)

/
├── data/                    # (opcional) CSVs originais utilizados
├── notebooks/               # Notebook exportado do Databricks
├── README.md                # Este arquivo

## Aluna

Natália Martins de Matos Nunes
