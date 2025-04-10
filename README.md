# MVP - Engenharia de Dados | Pós PUC-Rio

Este projeto foi desenvolvido como parte da disciplina de MVP do curso de Pós-Graduação em Ciência de Dados e Analytics da PUC-Rio. 
O objetivo foi construir um pipeline de dados completo, utilizando a arquitetura de camadas Bronze, Silver e Gold, com análises feitas na plataforma Databricks.

## Coleta dos Dados

Os dados utilizados neste projeto foram obtidos do Kaggle – Brazilian E-Commerce Public Dataset by Olist, um conjunto de dados reais e anonimizados fornecido pela empresa Olist, a maior loja de departamentos presente em marketplaces no Brasil.

O dataset contém informações sobre aproximadamente 100 mil pedidos realizados entre 2016 e 2018, abrangendo diversas dimensões do e-commerce, como:

Status do pedido
Informações de frete
Avaliações dos clientes
Pagamentos
Localização de clientes e vendedores
Características dos produtos
Os arquivos foram baixados em formato .csv e carregados manualmente na plataforma Databricks Community Edition, utilizando o menu de upload de dados. Após o upload, os arquivos foram movidos para diretórios organizados no DBFS e processados na camada Bronze do pipeline de dados.

A coleta também inclui o dataset de geolocalização por CEP, permitindo análises espaciais, e pode ser integrado com o dataset de funil de marketing da Olist, disponível separadamente.

Todos os dados são anonimizados e foram liberados para uso público com fins educacionais e de pesquisa.

## Objetivo

Este projeto tem como objetivo analisar a experiência do cliente a partir de dados de e-commerce da Olist, com foco em identificar padrões de satisfação e insatisfação relacionados a fatores como tempo de entrega, forma de pagamento, valor do pedido, localização geográfica e tipo de produto adquirido.

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

## Análise de Qualidade dos Dados

Antes das análises de negócio, foi realizada uma checagem básica de qualidade na tabela `gold_orders_analytics`. Os principais pontos observados foram:

- **Total de registros:** 118.310  
- **Pedidos únicos (`order_id`):** 98.666  
- **Avaliações ausentes (`review_score` nulo):** 978 registros (~0,8%)  
- **Pagamentos ausentes (`payment_value` nulo):** apenas 3 registros  
- **Categorias de produto ausentes:** 1.734 registros  
- **Notas fora do domínio esperado (1 a 5):** **0 registros**  
- **Duplicidade de `order_id`:** identificada, **mas esperada** devido à granularidade por item de pedido

A tabela está modelada em nível de item (`order_id` + `product_id`), portanto um mesmo pedido pode aparecer mais de uma vez se contiver múltiplos produtos.

Conclui-se que os dados são consistentes e adequados para as análises propostas.


## Principais Conclusões

Clientes insatisfeitos estão concentrados nas categorias mais populares, mas algumas menos conhecidas têm taxa de reclamação proporcional muito alta.
Tempo de entrega é o fator com maior correlação negativa com a nota de avaliação.
Pedidos de maior valor tendem a receber notas mais baixas.
Regiões Norte e Nordeste, além do RJ, apresentaram as maiores taxas proporcionais de insatisfação.
Forma de pagamento não influencia significativamente na satisfação do cliente.

## Autoavaliação
Durante o desenvolvimento deste MVP, acredito que consegui atingir com sucesso os objetivos definidos inicialmente: construir um pipeline de dados completo utilizando a arquitetura em camadas Bronze, Silver e Gold, com extração, transformação e carga dos dados no Databricks, culminando em análises que respondem a perguntas relevantes de negócio no contexto de e-commerce.

Apesar de já ter experiência com análise de dados, este projeto representou um grande desafio por exigir habilidades típicas de Engenharia de Dados, especialmente na modelagem e organização dos dados em múltiplas camadas, uso de Delta Lake, e aplicação correta das práticas de ETL em uma plataforma de nuvem.

As principais dificuldades enfrentadas foram:

Familiarização com a estrutura do Databricks Community Edition, incluindo armazenamento e caminhos corretos no DBFS.
A configuração do Git para manipulação de arquivos grandes.
Adaptação ao uso de PySpark e SQL sem recorrer a ferramentas mais comuns como pandas.

Por outro lado, o projeto me proporcionou grande aprendizado técnico e metodológico, além de reforçar a importância da organização dos dados para análises confiáveis. Também desenvolvi habilidades práticas de versionamento com Git e GitHub, e organização de repositório para projetos de dados.

Como trabalhos futuros, pretendo:

Implementar visualizações das análises com bibliotecas como matplotlib ou seaborn.
Expandir a modelagem com métricas de rentabilidade por categoria e região.
Automatizar parte do pipeline com workflows no Databricks ou scripts agendados.
Criar uma versão em inglês e incluir esse projeto no meu portfólio público.

Finalizo o projeto satisfeita com a entrega e com a evolução pessoal e profissional proporcionada por essa experiência.

## Estrutura de Diretórios (GitHub)

/
├── data/                    # (opcional) CSVs originais utilizados
├── notebooks/               # Notebook exportado do Databricks
├── README.md                # Este arquivo

## Aluna

Natália Martins de Matos Nunes
