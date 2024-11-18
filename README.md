-- Criação das tabelas

CREATE TABLE Clientes (
    cliente_id INT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    tipo_cliente VARCHAR(2) CHECK (tipo_cliente IN ('PJ', 'PF')),
    documento_cliente VARCHAR(20) NOT NULL
);

CREATE TABLE Pagamentos (
    pagamento_id INT PRIMARY KEY,
    cliente_id INT,
    metodo_pagamento VARCHAR(50),
    data_pagamento DATE,
    FOREIGN KEY (cliente_id) REFERENCES Clientes(cliente_id)
);

CREATE TABLE Pedidos (
    pedido_id INT PRIMARY KEY,
    cliente_id INT,
    data_pedido DATE,
    FOREIGN KEY (cliente_id) REFERENCES Clientes(cliente_id)
);

CREATE TABLE Entregas (
    entrega_id INT PRIMARY KEY,
    pedido_id INT,
    status_entrega VARCHAR(50),
    codigo_rastreio VARCHAR(100),
    FOREIGN KEY (pedido_id) REFERENCES Pedidos(pedido_id)
);

CREATE TABLE Fornecedores (
    fornecedor_id INT PRIMARY KEY,
    nome_fornecedor VARCHAR(255)
);

CREATE TABLE Produtos (
    produto_id INT PRIMARY KEY,
    nome_produto VARCHAR(255),
    preco DECIMAL(10, 2),
    fornecedor_id INT,
    FOREIGN KEY (fornecedor_id) REFERENCES Fornecedores(fornecedor_id)
);

CREATE TABLE Estoque (
    estoque_id INT PRIMARY KEY,
    produto_id INT,
    quantidade_estoque INT,
    FOREIGN KEY (produto_id) REFERENCES Produtos(produto_id)
);

-- Inserção de dados de exemplo

INSERT INTO Clientes (cliente_id, nome, tipo_cliente, documento_cliente) 
VALUES (1, 'João Silva', 'PF', '123.456.789-00'),
       (2, 'Empresa X', 'PJ', '12.345.678/0001-99');

INSERT INTO Pagamentos (pagamento_id, cliente_id, metodo_pagamento, data_pagamento)
VALUES (1, 1, 'Cartão de Crédito', '2024-11-10'),
       (2, 2, 'Boleto', '2024-11-12');

INSERT INTO Pedidos (pedido_id, cliente_id, data_pedido)
VALUES (1, 1, '2024-11-10'),
       (2, 2, '2024-11-11');

INSERT INTO Entregas (entrega_id, pedido_id, status_entrega, codigo_rastreio)
VALUES (1, 1, 'Em Transito', 'R123456789'),
       (2, 2, 'Entregue', 'R987654321');

INSERT INTO Fornecedores (fornecedor_id, nome_fornecedor)
VALUES (1, 'Fornecedor A'),
       (2, 'Fornecedor B');

INSERT INTO Produtos (produto_id, nome_produto, preco, fornecedor_id)
VALUES (1, 'Produto X', 100.00, 1),
       (2, 'Produto Y', 50.00, 2);

INSERT INTO Estoque (estoque_id, produto_id, quantidade_estoque)
VALUES (1, 1, 100),
       (2, 2, 200);
SELECT c.nome, COUNT(p.pedido_id) AS total_pedidos
FROM Clientes c
LEFT JOIN Pedidos p ON c.cliente_id = p.cliente_id
GROUP BY c.nome;
-- Supondo que exista uma tabela de vendedores
SELECT v.nome_vendedor, f.nome_fornecedor
FROM Vendedores v
JOIN Fornecedores f ON v.vendedor_id = f.fornecedor_id;
SELECT p.nome_produto, f.nome_fornecedor, e.quantidade_estoque
FROM Produtos p
JOIN Fornecedores f ON p.fornecedor_id = f.fornecedor_id
JOIN Estoque e ON p.produto_id = e.produto_id;

SELECT f.nome_fornecedor, p.nome_produto
FROM Produtos p
JOIN Fornecedores f ON p.fornecedor_id = f.fornecedor_id;
# Projeto Lógico de Banco de Dados - E-commerce

## Descrição

Este projeto visa modelar o banco de dados lógico de um sistema de e-commerce, com ênfase nas tabelas de clientes, pedidos, pagamentos, entregas, fornecedores, produtos e estoque. O objetivo é mapear as relações entre as entidades do sistema, assegurando que os dados estejam estruturados de maneira eficiente para suportar as operações de um e-commerce.

### Estrutura do Banco de Dados

O banco de dados é composto pelas seguintes tabelas:

- **Clientes**: Armazena informações de clientes (PJ ou PF).
- **Pagamentos**: Armazena formas de pagamento dos clientes.
- **Pedidos**: Detalha os pedidos realizados pelos clientes.
- **Entregas**: Contém informações sobre o status e código de rastreio das entregas.
- **Fornecedores**: Registra os fornecedores dos produtos.
- **Produtos**: Contém informações sobre os produtos comercializados.
- **Estoque**: Mantém o controle de quantidade de estoque de produtos.

### Consultas SQL

Diversas consultas SQL foram criadas para permitir a análise detalhada dos dados, incluindo:

- Recuperação do número de pedidos por cliente.
- Análise de relacionamento entre vendedores e fornecedores.
- Relações entre produtos, fornecedores e estoque.

### Como Rodar o Projeto

1. Clone o repositório.
2. Execute o script SQL para criar o banco de dados.
3. Utilize as queries fornecidas para explorar os dados.

