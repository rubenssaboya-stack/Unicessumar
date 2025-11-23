# Unicessumar

# Tabela: Categoria de Produtos Gráficos
CREATE TABLE categoria (
id_categoria INTEGER PRIMARY KEY SERIAL,
descricao_categoria VARCHAR (100)  NOT NULL
);

# Tabela: UF (Unidade Fortaleza) 
CREATE TABLE uf (
id_uf INTEGER PRIMARY KEY SERIAL,
sigla CHAR(2) NOT NULL UNIQUE,
descrição_uf VARCHAR(100) NOT NULL
);

#Tabela: Cidade
CREATE TABLE cidade (

id_cidade INTEGER PRIMARY KEY SERIAL,
id_uf_fk INTEGER NOT NULL, 
descricao_cidade VARCHAR (100) NOT NULL,
FOREIGN KEY (id_uf_fk) REFERENCES uf (id_uf)
);

#Tabela: Produtos Gráficos
CREATE TABLE produto (
id_produto INTEGER PRIMARY KEY SERIAL,
nome_produto VARCHAR(100) NOT NULL,
descricao_do_produto TEXT,
id_categoria_fk INTEGER NOT NULL,
preco_unitario DECIMAL (10,2) NOT NULL,
quantidade_estoque INTEGER  NOT NULL,
tipo_papel VARCHAR (100), 
acabamento VARCHAR (100),
observacacoes TEXT,
FOREIGN KEY (id_categoria_fk) REFERENCES categoria (id_categoria)
);

# Tabela: Clientes
CREATE TABLE cliente (
id_cliente INTEGER PRIMARY KEY SERIAL,
nome_completo VARCHAR (100) NOT NULL,
cpf_cnpj VARCHAR (14) NOT NULL UNIQUE,
telefone VARCHAR (20) NOT NULL,
email VARCHAR (100) ,
endereco VARCHAR (150) NOT NULL,
id_uf_fk INTEGER NOT NULL,
id_cidade_fk INTEGER NOT NULL,
cep VARCHAR (10) ,
FOREIGN KEY (id_uf_fk) REFERENCES uf (id_uf),
FOREIGN KEY (id_cidade_fk) REFERENCES cidade (id_cidade)
);

# Tabela: Pedidos
CREATE TABLE pedido (
id_pedido INTEGER PRIMARY KEY SERIAL,
id_cliente_fk INTEGER NOT NULL,
data_pedido DATE NOT NULL, 
date_entrega DATE,
status VARCHAR (50) NOT NULL,
total_pedido DECIMAL (10,2) NOT NULL,
observacao TEXT,
FOREIGN KEY (id_cliente_fk) REFERENCES cliente (id_cliente)
);

# Tabela: Itens do Pedido
CREATE TABLE itens_produto (
id_itens_pedido INTEGER PRIMARY KEY SERIAL,
id_pedido_fk INTEGER NOT NULL,
id_produto_fk INTEGER NOT NULL,
descricao_personalizada TEXT,
valor_unitario DECIMAL (10,2) NOT NULL,
valor_total DECIMAL (10,2) NOT NULL,
FOREIGN (id_pedido_fk) REFERENCES pedido (id_pedido),
FOREIGN (id_produto_fk) REFERENCES produto (id_produto)
);
