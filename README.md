Projeto-BD
Primeiro projeto de Banco de dados I -Unicap

MODELO ENTIDADE RELACIONAMENTO: 
https://app.brmodeloweb.com/#!/publicview/66f44f77200d3a7176c01e45

![image](https://github.com/user-attachments/assets/3849f5ce-c2d8-4d38-bfaa-433ccbaa92dd)


MODELO RELACIONAL: 

https://dbdiagram.io/d/MR-projeto-BD-I-66f4c56c3430cb846ca64a79

![image](https://github.com/user-attachments/assets/f0c9e259-ed99-4e60-90d5-08c606b503b7)


PERGUNTAS QUE AGREGAM VALOR AO NEGOCIO:

1.⁠ ⁠Qual o local mais popular para eventos?

2.⁠ ⁠Quais eventos possuem maior taxa de confirmação?

3.⁠ ⁠Quais são os restaurantes mais bem avaliados?

4.⁠ ⁠Quais são os clientes mais frequentes?

5.⁠ ⁠Qual é a especialidade médica mais procurada?


MODELO DDL: 

-- Tabela Local
CREATE TABLE Local (
    id_local INT PRIMARY KEY,
    rua_local VARCHAR(255),
    bairro_local VARCHAR(255),
    cidade_local VARCHAR(255),
    estado_local VARCHAR(50),
    numero_local INT,
    complemento_local VARCHAR(255),
    capacidade_local INT
);

-- Tabela Restaurante
CREATE TABLE Restaurante (
    id_restaurante INT PRIMARY KEY,
    nome VARCHAR(255),
    id_local INT,
    FOREIGN KEY (id_local) REFERENCES Local(id_local)
);

-- Tabela Cozinha
CREATE TABLE Cozinha (
    id INT PRIMARY KEY,
    id_restaurante INT,
    FOREIGN KEY (id_restaurante) REFERENCES Restaurante(id_restaurante)
);

-- Tabela Cozinheiro
CREATE TABLE Cozinheiro (
    id INT PRIMARY KEY,
    nome VARCHAR(255),
    id_restaurante INT,
    FOREIGN KEY (id_restaurante) REFERENCES Restaurante(id_restaurante)
);

-- Tabela Gerente
CREATE TABLE Gerente (
    id INT PRIMARY KEY,
    nome VARCHAR(255),
    id_restaurante INT,
    FOREIGN KEY (id_restaurante) REFERENCES Restaurante(id_restaurante)
);

-- Tabela Garcom
CREATE TABLE Garcom (
    id INT PRIMARY KEY,
    nome VARCHAR(255),
    id_restaurante INT,
    FOREIGN KEY (id_restaurante) REFERENCES Restaurante(id_restaurante)
);

-- Tabela Mesa
CREATE TABLE Mesa (
    id_mesa INT PRIMARY KEY,
    descricao VARCHAR(255),
    id_restaurante INT,
    FOREIGN KEY (id_restaurante) REFERENCES Restaurante(id_restaurante)
);

-- Tabela Pedido
CREATE TABLE Pedido (
    id_pedido INT PRIMARY KEY,
    id_mesa INT,
    descricao VARCHAR(255),
    FOREIGN KEY (id_mesa) REFERENCES Mesa(id_mesa)
);

-- Tabela Item_Pedido
CREATE TABLE Item_Pedido (
    id INT PRIMARY KEY,
    id_pedido INT,
    FOREIGN KEY (id_pedido) REFERENCES Pedido(id_pedido)
);

-- Tabela Cliente
CREATE TABLE Cliente (
    id INT PRIMARY KEY,
    nome VARCHAR(255),
    id_mesa INT,
    FOREIGN KEY (id_mesa) REFERENCES Mesa(id_mesa)
);

-- Tabela Evento
CREATE TABLE Evento (
    id_evento INT PRIMARY KEY,
    nome_evento VARCHAR(255),
    data_inicio DATE,
    data_fim DATE,
    tipo_evento VARCHAR(255),
    valor_evento DECIMAL(10, 2),
    descricao_evento VARCHAR(255),
    qnt_maxima INT,
    id_local INT,
    FOREIGN KEY (id_local) REFERENCES Local(id_local)
);

-- Tabela Palestrante
CREATE TABLE Palestrante (
    id_palestrante INT PRIMARY KEY,
    nome VARCHAR(255),
    especialidade VARCHAR(255)
);

-- Tabela Sessao
CREATE TABLE Sessao (
    id_sessao INT PRIMARY KEY,
    hora_inicio TIME,
    hora_fim TIME,
    id_evento INT,
    id_palestrante INT,
    FOREIGN KEY (id_evento) REFERENCES Evento(id_evento),
    FOREIGN KEY (id_palestrante) REFERENCES Palestrante(id_palestrante)
);

-- Tabela Inscricao
CREATE TABLE Inscricao (
    id_inscricao INT PRIMARY KEY,
    id_evento INT,
    id_pessoa INT,
    status VARCHAR(255),
    metodo_pagamento VARCHAR(255),
    FOREIGN KEY (id_evento) REFERENCES Evento(id_evento),
    FOREIGN KEY (id_pessoa) REFERENCES Pessoa(id_pessoa)
);

-- Tabela Pessoa
CREATE TABLE Pessoa (
    id_pessoa INT PRIMARY KEY,
    nome VARCHAR(255),
    cpf VARCHAR(14),
    email VARCHAR(255),
    telefone VARCHAR(20),
    data_nascimento DATE,
    genero VARCHAR(50),
    profissao VARCHAR(255)
);

-- Tabela Clinica
CREATE TABLE Clinica (
    id_clinica INT PRIMARY KEY,
    nome_clinica VARCHAR(255),
    local_clinica VARCHAR(255),
    telefone_clinica VARCHAR(20),
    especialidade_clinica VARCHAR(255)
);

-- Tabela Paciente
CREATE TABLE Paciente (
    id_paciente INT PRIMARY KEY,
    nome_paciente VARCHAR(255),
    sexo_paciente VARCHAR(50),
    idade_paciente INT,
    cpf_paciente VARCHAR(14)
);

-- Tabela Medico
CREATE TABLE Medico (
    id_medico INT PRIMARY KEY,
    nome_medico VARCHAR(255),
    especializacao VARCHAR(255),
    crm_medico VARCHAR(20)
);



-- Tabela Recepcao
CREATE TABLE Recepcao (
    id_recepcao INT PRIMARY KEY,
    nome_recepcionista VARCHAR(255),
    capacidade_recepcao INT,
    id_clinica INT,
    FOREIGN KEY (id_clinica) REFERENCES Clinica(id_clinica)
);

-- Tabela Consulta
CREATE TABLE Consulta (
    id_consulta INT PRIMARY KEY,
    data_consulta DATE,
    tipo_consulta VARCHAR(255),
    status_consulta VARCHAR(255),
    id_recepcao INT,
    id_medico INT,
    id_paciente INT,
    FOREIGN KEY (id_recepcao) REFERENCES Recepcao(id_recepcao),
    FOREIGN KEY (id_medico) REFERENCES Medico(id_medico),
    FOREIGN KEY (id_paciente) REFERENCES Paciente(id_paciente)
);

-- Tabela Realiza (Relacionamento entre Pessoa e Evento)
CREATE TABLE Realiza (
    id_pessoa INT,
    id_evento INT,
    PRIMARY KEY (id_pessoa, id_evento),
    FOREIGN KEY (id_pessoa) REFERENCES Pessoa(id_pessoa),
    FOREIGN KEY (id_evento) REFERENCES Evento(id_evento)
);

