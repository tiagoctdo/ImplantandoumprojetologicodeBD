# ImplantandoumprojetologicodeBD
Desafio Criando e Implantando um projeto Logico de Banco de Dados

Desafio proposto pelo bootcamp Potência Tech Powered by iFood | Ciência de Dados com Python!
modelagem de banco de dados em SQL

MySQL 8.0.34


![ecommerce](https://github.com/tiagoctdo/ImplantandoumprojetologicodeBD/assets/102422491/c0398e14-8489-4d0a-85d2-4615f2e5c639)

DROP DATABASE IF EXISTS ecommerce;

-- Create the database
CREATE DATABASE ecommerce;
USE ecommerce;

-- Table: cliente
CREATE TABLE cliente (
    idCliente INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    dataNascimento DATE NOT NULL,
    primeiroNome VARCHAR(50) NOT NULL,
    sobrenomecliente CHAR(6),
    CPFCNPJ VARCHAR(14),
    endereco VARCHAR(50),
    complemento VARCHAR (25),
    cidade VARCHAR (25),
    UF VARCHAR (2)
);


-- Table: pagamentos 
CREATE TABLE pagamentos (
    idPagamento INT AUTO_INCREMENT NOT NULL PRIMARY KEY,	
    tipoPagamento ENUM('PIX', 'Boleto', 'Cartão', 'Dois Cartões') DEFAULT 'Cartão'
);

-- Table: pedidos 
CREATE TABLE pedidos (
    idPedido INT AUTO_INCREMENT PRIMARY KEY,
    idpedidopagamento int not null,
    idPedidoCliente INT NOT NULL,
    idPedidoEntrega INT NOT NULL,
    statusPEDIDO VARCHAR(45),
    descricao VARCHAR(255),
    frete FLOAT DEFAULT 10
);

-- Table: fornecedor
CREATE TABLE fornecedores (
    idFornecedor INT AUTO_INCREMENT PRIMARY KEY,
    cnpj CHAR(18) NOT NULL, -- Increased column size to accommodate CNPJ values
    razaoSocial VARCHAR(50) NOT NULL,
    contato CHAR(11) NOT NULL,
    quantidade decimal(10,2),
    Produto VARCHAR(45),
    CONSTRAINT unique_cnpj_fornecedor UNIQUE (cnpj),
    CONSTRAINT unique_razaoSocial_fornecedor UNIQUE (razaoSocial)
);

-- Table: produtos 
CREATE TABLE produtos (
    idProduto INT AUTO_INCREMENT PRIMARY KEY,
    nomeProduto VARCHAR(50) NOT NULL,
    categoria ENUM('Eletrônico', 'Vestimenta', 'Brinquedos', 'Alimentos', 'Móveis') NOT NULL,
    localizacaoestoque VARCHAR(45),
    descricao VARCHAR(255),
    valorvenda FLOAT NOT NULL,
    custoproduto DECIMAL(10, 2),
    markup DECIMAL(10,2)
);


-- Table: entregas 
CREATE TABLE entrega (
    idEntrega INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    statusEntrega ENUM('Em andamento', 'Em processamento', 'Enviado', 'Entregue') DEFAULT 'Em processamento',
    codRastreio CHAR(10) NOT NULL,
    CONSTRAINT unique_codRastreio UNIQUE (codRastreio)
);



--- total de clientes
SELECT idCliente, COUNT(idCliente) AS TotaldeClientes
FROM cliente
GROUP BY idCliente;

--- VGV vendido por produto.
SELECT nomeProduto, SUM(valorvenda) AS VGVVENDIDO
FROM produtos
GROUP BY nomeProduto;

