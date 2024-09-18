# teste-aula
Aula
teste aula


# 1-  Introdução 

# 2-  Descrição do sistemas 

# 3-  Visão Geral do sistemas 

# 4-  Diagrama ER 



```mermaid

erDiagram
    Produto {
        int codigo_produto PK
        string descricao
        decimal preco
        string marca
        string categoria
        int quantidade_estoque
    }

    Servico {
        int codigo_servico PK
        string descricao
        decimal preco
        int duracao
    }

    Cliente {
        int codigo_cliente PK
        string nome
        string endereco
        string telefone
        string email
    }

    Animal {
        int codigo_animal PK
        string nome
        string especie
        string raca
        date data_nascimento
        int codigo_cliente FK
    }

    Compra {
        int numero_compra PK
        date data_compra
        decimal valor_total
        int codigo_cliente FK
    }

    Item_Compra {
        int id PK
        int quantidade
        decimal desconto
        int codigo_produto FK
        int numero_compra FK
    }

    Agendamento {
        int id PK
        datetime data_hora
        int codigo_servico FK
        int codigo_animal FK
    }

    Fornecedor {
        int codigo_fornecedor PK
        string nome
        string contato
    }

    Pedido_Compra {
        int numero_pedido PK
        date data_pedido
        int codigo_fornecedor FK
    }

    Item_Pedido {
        int id PK
        int quantidade
        int codigo_produto FK
        int numero_pedido FK
    }

    Pagamento {
        int id PK
        date data_pagamento
        decimal valor
        string forma_pagamento
        int numero_compra FK
    }

    Consulta {
        int id PK
        date data_consulta
        string motivo
        string tratamento
        int codigo_animal FK
    }

    Cliente --|{ Compra : realiza
    Animal --|{ Compra : possui
    Produto --|{ Compra : contém via Item_Compra
    Servico --|{ Agendamento : oferece
    Animal --|{ Agendamento : recebe
    Fornecedor --|{ Pedido_Compra : realiza
    Produto --|{ Pedido_Compra : solicita via Item_Pedido
    Compra --|{ Pagamento : possui
    Animal --|{ Consulta : possui
```




# 5- Diagrama de classe 
```
classDiagram
  class Produto {
    - codigo_produto: int
    - descricao: string
    - preco: decimal
    - marca: string
    - categoria: string
    - quantidade_estoque: int
  }

  class Servico {
    - codigo_servico: int
    - descricao: string
    - preco: decimal
    - duracao: int
  }

  class Cliente {
    - codigo_cliente: int
    - nome: string
    - endereco: string
    - telefone: string
    - email: string
    - animais: Animal[]
    - compras: Compra[]
  }

  class Animal {
    - codigo_animal: int
    - nome: string
    - especie: string
    - raca: string
    - data_nascimento: date
    - dono: Cliente
    - consultas: Consulta[]
  }

  class Compra {
    - numero_compra: int
    - data_compra: date
    - valor_total: decimal
    - cliente: Cliente
    - itens: ItemCompra[]
    - pagamento: Pagamento
  }

  class ItemCompra {
    - id: int
    - quantidade: int
    - desconto: decimal
    - produto: Produto
    - compra: Compra
  }

  -- ... (continuar com as outras classes)

  Cliente "1" -- "*" Animal : tem
  Cliente "1" -- "*" Compra : realiza
  Produto "1" -- "*" ItemCompra : compõe
  Compra "1" -- "*" ItemCompra : contém
  -- ... (continuar com os outros relacionamentos)
  ```


# Script SQL 

````SQL 

CREATE DATABASE pet_shop;
USE pet_shop;

-- Criação das tabelas
CREATE TABLE Produto (
    codigo_produto INT PRIMARY KEY,
    descricao VARCHAR(100),
    preco DECIMAL(10,2),
    marca VARCHAR(50),
    categoria VARCHAR(50),
    quantidade_estoque INT
);

CREATE TABLE Servico (
    codigo_servico INT PRIMARY KEY,
    descricao VARCHAR(100),
    preco DECIMAL(10,2),
    duracao INT
);

-- ... (continuar criando as tabelas de acordo com o diagrama)

-- Criação das chaves estrangeiras
ALTER TABLE Animal ADD CONSTRAINT fk_animal_cliente FOREIGN KEY (codigo_cliente) REFERENCES Cliente(codigo_cliente);
-- ... (continuar criando as outras chaves estrangeiras)

```