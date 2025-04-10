# Catálogo de Dados - Projeto MVP Olist

Este catálogo apresenta uma descrição detalhada das tabelas utilizadas no projeto, com informações sobre colunas, chaves primárias (PK), chaves estrangeiras (FK), tipos de dados, descrições e domínios esperados para facilitar a compreensão do modelo de dados implementado.

---

## A. Tabela de Fatos `gold_orders_analytics`

| Coluna                         | Tipo      | PK/FK | Descrição                                                           | Domínio / Valores esperados         |
|-------------------------------|-----------|-------|------------------------------------------------------------------------|------------------------------------|
| `order_id`                    | string    | PK    | Identificador do pedido                                               | UUID                               |
| `customer_id`                 | string    | FK    | Referência à tabela de clientes                                       | UUID                               |
| `product_id`                  | string    | FK    | Referência à tabela de produtos                                       | UUID                               |
| `review_score`                | integer   |       | Nota de avaliação dada pelo cliente                                  | 1 a 5                              |
| `product_category_name_english` | string  |       | Categoria traduzida do produto                                       | Nomes de categorias em inglês      |
| `payment_type`                | string    |       | Forma de pagamento utilizada no pedido                               | credit_card, boleto, etc.          |
| `payment_value`               | float     |       | Valor total pago pelo cliente                                        | 0 a 10000+                         |
| `customer_state`              | string    |       | Estado de origem do cliente                                          | SP, RJ, MG, etc.                   |
| `order_purchase_timestamp`    | timestamp |       | Data/hora da compra                                                  | yyyy-mm-dd hh:mm:ss                |
| `order_delivered_customer_date` | timestamp |     | Data/hora da entrega                                                 | yyyy-mm-dd hh:mm:ss                |
| `delivery_days`               | integer   |       | Diferença entre entrega e compra (dias)                             | >= 0                               |

---

## B. Tabela de Dimensão `silver.customers`

| Coluna           | Tipo    | PK/FK | Descrição                                      |
|------------------|---------|-------|------------------------------------------------|
| `customer_id`    | string  | PK    | Identificador único do cliente                 |
| `customer_state` | string  |       | Estado do cliente (utilizado para segmentação) |

---

## C. Tabela de Dimensão `silver.products`

| Coluna                          | Tipo    | PK/FK | Descrição                                     |
|---------------------------------|---------|-------|-----------------------------------------------|
| `product_id`                    | string  | PK    | Identificador do produto                      |
| `product_category_name_english`| string  |       | Categoria traduzida                           |

---

## D. Tabela de Dimensão `silver.order_reviews`

| Coluna         | Tipo    | PK/FK | Descrição                              |
|----------------|---------|-------|----------------------------------------|
| `order_id`     | string  | PK    | Referência ao pedido avaliado          |
| `review_score` | integer |       | Nota de avaliação de 1 a 5             |

---

## E. Tabela de Dimensão `silver.order_payments`

| Coluna          | Tipo    | PK/FK | Descrição                                  |
|-----------------|---------|-------|--------------------------------------------|
| `order_id`      | string  | PK    | Referência ao pedido pago                  |
| `payment_type`  | string  |       | Tipo de pagamento (boleto, cartão, etc.)   |
| `payment_value` | float   |       | Valor pago pelo cliente                    |

---

Este catálogo pode ser expandido com informações das camadas Bronze e Silver conforme necessidade. Ele visa documentar os principais dados utilizados na camada Gold e como eles se relacionam com outras tabelas do pipeline.
