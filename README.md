# Hospital Fundamental
Um pequeno hospital local busca desenvolver um novo sistema que atenda melhor às suas necessidades. Atualmente, parte da operação ainda se apoia em planilhas e arquivos antigos, mas espera-se que esses dados sejam transferidos para o novo sistema assim que ele estiver funcional. Neste momento, é necessário analisar com cuidado as necessidades desse cliente e sugerir uma estrutura de banco de dados adequada por meio de um Diagrama Entidade-Relacionamento.

## Estudo de caso

O hospital necessita de um sistema para sua área clínica que ajude a controlar consultas realizadas. Os médicos podem ser generalistas, especialistas ou residentes e têm seus dados pessoais cadastrados em planilhas digitais. Cada médico pode ter uma ou mais especialidades, que podem ser pediatria, clínica geral, gastroenterologia e dermatologia. Alguns registros antigos ainda estão em formulário de papel, mas será necessário incluir esses dados no novo sistema.

Os pacientes também precisam de cadastro, contendo dados pessoais (nome, data de nascimento, endereço, telefone e e-mail), documentos (CPF e RG) e convênio. Para cada convênio, são registrados nome, CNPJ e tempo de carência.

As consultas também têm sido registradas em planilhas, com data e hora de realização, médico responsável, paciente, valor da consulta ou nome do convênio, com o número da carteira. Também é necessário indicar na consulta qual a especialidade buscada pelo paciente.

Deseja-se ainda informatizar a receita do médico, de maneira que, no encerramento da consulta, ele possa registrar os medicamentos receitados, a quantidade e as instruções de uso. A partir disso, espera-se que o sistema imprima um relatório da receita ao paciente ou permita sua visualização via internet.

## Requisitos do Hospital

**RF001** O sistema deve permitir o cadastro dos profissionais do Hospital, contendo os dados pessoais como nome, CPF, data de nascimento, endereço, telefone e e-mail; seu cargo e suas especialidades.

**RF002** O atendente deve ser capaz de agendar uma consulta para o paciente com os dados: data e hora da realização, 
profissional responsável, paciente, valor da consulta ou convênio e especialidade buscada pelo paciente.

**RF003** O atendente deve ser capaz de cadastrar o paciente, com os dados pessoais como nome, data de nascimento, endereço, telefone, e-mail; documentos (CPF e RG) e os dados do convênio, como número da carteira.

**RF004** O sistema deve registrar o convênio de cada paciente com os dados: nome, número de carteira, CNPJ e tempo de carência.

**RF005** O paciente deve ser capaz de consultar os dados da sua consulta usando seu CPF, por meio do portal online da clínica.

**RF006** O médico deve ser capaz de encerrar a consulta registrando os medicamentos receitados, a quantidade e as instruções de uso.

**RF007** O sistema deve permitir a impressão de relatórios com os dados das consultas dos pacientes.

## Diagrama ER
![alt text](image.png)

# Os Segredos do Hospital
Após a primeira versão do projeto de banco de dados para o sistema hospitalar, notou-se a necessidade de expansão das funcionalidades, incluindo alguns requisitos essenciais a essa versão do software. As funcionalidades em questão são para o controle na internação de pacientes. Será necessário expandir o Modelo ER desenvolvido e montar o banco de dados, criando as tabelas para o início dos testes.

## Estudo de caso
Considere a seguinte descrição e o diagrama ER abaixo:

No hospital, as internações têm sido registradas por meio de formulários eletrônicos que gravam os dados em arquivos. 

Para cada internação, são anotadas a data de entrada, a data prevista de alta e a data efetiva de alta, além da descrição textual dos procedimentos a serem realizados. 

As internações precisam ser vinculadas a quartos, com a numeração e o tipo. 

Cada tipo de quarto tem sua descrição e o seu valor diário (a princípio, o hospital trabalha com apartamentos, quartos duplos e enfermaria).

Também é necessário controlar quais profissionais de enfermaria estarão responsáveis por acompanhar o paciente durante sua internação. Para cada enfermeiro(a), é necessário nome, CPF e registro no conselho de enfermagem (CRE).

A internação, obviamente, é vinculada a um paciente – que pode se internar mais de uma vez no hospital – e a um único médico responsável.

## Requisitos do Hospital

**RF001** O sistema deve permitir o cadastro dos profissionais do Hospital, contendo os dados pessoais como nome, CPF, data de nascimento, endereço, telefone e e-mail; seu cargo e suas especialidades.

**RF002** O atendente deve ser capaz de agendar uma consulta para o paciente com os dados: data e hora da realização, 
profissional responsável, paciente, valor da consulta ou convênio e especialidade buscada pelo paciente.

**RF003** O atendente deve ser capaz de cadastrar o paciente, com os dados pessoais como nome, data de nascimento, endereço, telefone, e-mail; documentos (CPF e RG) e os dados do convênio, como número da carteira.

**RF004** O sistema deve registrar o convênio de cada paciente com os dados: nome, número de carteira, CNPJ e tempo de carência.

**RF005** O paciente deve ser capaz de consultar os dados da sua consulta usando seu CPF, por meio do portal online da clínica.

**RF006** O médico deve ser capaz de encerrar a consulta registrando os medicamentos receitados, a quantidade e as instruções de uso.

**RF007** O sistema deve permitir a impressão de relatórios com os dados das consultas dos pacientes.

**RF008** O sistema deve permitir o registro das internações do paciente, com os dados: data de entrada no hospital, data prevista de alta, data da alta, descrição dos procedimentos, dados do quarto, enfermeiro, médico e paciente.

**RF009** O sistema deve permitir o cadastro dos quartos existentes no hospital, com a numeração, a descrição do quarto, valor diário e tipo do quarto.

**RF010** O sistema deve permitir o registro dos profissionais de enfermaria contendo os dados: nome, CPF e registro no conselho de enfermagem (CRE).

## Diagrama ER
![ModeloHospital](https://github.com/Leuquary/banco-dados-hospital/assets/111248276/b6744038-adb5-466d-b6f1-5aa6137cd29e)

## Código SQL

```sql
create database hospital;
use hospital;

create table medico (
     codigo_medico int primary key,
     nome_medico varchar(50) not null,
     cpf_medico varchar(15) unique not null,
     rg_medico varchar(9) unique not null,
     cargo_medico varchar(20) not null,
     salario_medico decimal(5,2) not null,
     crm_medico varchar(20) not null,
     data_nasc_medico date not null
);

create table especialidade_medico(
     codigo_medico int not null,
     codigo_especialidade int not null
);

create table paciente (
     codigo_paciente int primary key,
     nome_paciente varchar(50) not null,
     cpf_paciente varchar(11) unique not null, 
     rg_paciente varchar(9) unique not null, 
     telefone_paciente varchar(11) not null,
     email_paciente varchar(50) unique not null,
     data_nasc_paciente date not null,
     numero_carteira_convenio int not null
);

create table convenio (
     numero_carteira int primary key, 
     nome_convenio varchar(50) not null,
     tempo_carencia varchar(10) not null,
     cnpj_convenio varchar(14) unique not null
);

create table consulta(
     codigo_consulta int primary key,
     data_consulta date not null,
     horario_consulta time not null,
     valor_consulta decimal(5,2) not null,
     forma_pagamento varchar(20) not null,
     codigo_paciente int not null,
     codigo_medico int not null, 
     codigo_especialidade int not null,
     numero_carteira_convenio int
);

create table especialidade(
    codigo_especialidade int primary key,
    descricao_especialidade varchar(50) not null
);

create table receita(
    codigo_receita int primary key,
    nome_medicamento varchar(100) not null,
    instrucoes_medicamento varchar(255) not null,
    qtd_medicamento int not null,
    codigo_consulta int not null
);

create table endereco(
    codigo_endereco int primary key,
    rua varchar(100) not null,
    bairro varchar(100) not null,
    cep varchar(9) not null,
    numero int not null,
    complemento varchar(100),
    codigo_paciente int not null
);

create table internacao(
    codigo_internacao int primary key,
    data_prevista_alta date not null,
    data_entrada date not null,
    data_alta date,
    codigo_medico int not null,
    numero_quarto int not null,
    codigo_paciente int not null,
    numero_carteira_convenio int
);

create table quarto(
    numero_quarto int primary key,
    codigo_tipo_quarto int not null
);

create table procedimento(
    codigo_procedimento int primary key,
    nome_procedimento varchar(50) not null,
    descricao_procedimento varchar(100) not null
);

create table procedimento_internacao(
    codigo_internacao int not null,
    codigo_procedimento int not null
);

create table enfermeiro(
    codigo_enfermeiro int primary key,
    nome_enfermeiro varchar(50) not null,
    rg_enfermeiro varchar(9) unique not null,
    cpf_enfermeiro varchar(15) unique not null,
    cre_enfermeiro varchar(20) unique not null,
    data_nasc_enfermeiro date not null
);

create table tipo_quarto(
    codigo_tipo_quarto int primary key,
    diaria_quarto decimal(5,2) not null,
    descricao_quarto varchar(200) not null
);

create table enfermeiro_internacao(
    codigo_enfermeiro int not null,
    codigo_internacao int not null
);

/*relacionando consulta e especialidade*/
alter table consulta add foreign key fk_codigo_especialidade (codigo_especialidade) references especialidade(codigo_especialidade);

/*relacionando consulta e médico*/
alter table consulta add foreign key fk_codigo_medico (codigo_medico) references medico(codigo_medico);

/*relacionando consulta paciente*/
alter table consulta add foreign key fk_codigo_paciente (codigo_paciente) references paciente(codigo_paciente);

/*relacionando consulta e receita*/
alter table receita add foreign key fk_codigo_consulta (codigo_consulta) references consulta(codigo_consulta);

/*relacionando consulta e convenio*/
alter table consulta add foreign key fk_numero_carteira_convenio (numero_carteira_convenio) references convenio(numero_carteira);

/*relacionando paciente e convênio*/
alter table paciente add foreign key fk_numero_carteira_convenio (numero_carteira_convenio) references convenio(numero_carteira);

/*relacionando paciente e endereço*/
alter table endereco add foreign key fk_codigo_paciente (codigo_paciente) references paciente(codigo_paciente);

/*relacionando especialidade e médico*/
alter table especialidade_medico add foreign key fk_codigo_medico (codigo_medico) references medico(codigo_medico);
alter table especialidade_medico add foreign key fk_codigo_especialidade (codigo_especialidade) references especialidade(codigo_especialidade);

/*relacionando internação e quarto*/
alter table internacao add foreign key fk_numero_quarto (numero_quarto) references quarto(numero_quarto);

/*relacionando internação e procedimento*/
alter table procedimento_internacao add foreign key fk_codigo_internacao (codigo_internacao) references internacao(codigo_internacao);
alter table procedimento_internacao add foreign key fk_codigo_procedimento (codigo_procedimento) references procedimento(codigo_procedimento);

/*relacionando internação e médico*/	
alter table internacao add foreign key fk_codigo_medico (codigo_medico) references medico(codigo_medico);

/*relacionando internação e enfermeiro*/
alter table enfermeiro_internacao add foreign key fk_codigo_enfermeiro (codigo_enfermeiro) references enfermeiro(codigo_enfermeiro);
alter table enfermeiro_internacao add foreign key fk_codigo_internacao (codigo_internacao) references internacao(codigo_internacao);

/*relacionando internação e paciente*/
alter table internacao add foreign key fk_codigo_paciente (codigo_paciente) references paciente(codigo_paciente);

/*relacionando internação e convênio*/
alter table internacao add foreign key fk_numero_carteira_convenio (numero_carteira_convenio) references convenio(numero_carteira);

/*relacionando quarto e tipo*/
alter table quarto add foreign key fk_tipo_quarto (codigo_tipo_quarto) references tipo_quarto(codigo_tipo_quarto);
```

# O Prisioneiro dos Dados
Com o banco de dados para o sistema hospitalar completamente montado, é necessário incluir dados para realizar os devidos testes e validar sua viabilidade quanto ao sistema. Nesta etapa, também é importante realizar a separação de alguns scripts iniciais para o banco, com os dados que serão necessários a um povoamento inicial do sistema.

- Inclua ao menos dez médicos de diferentes especialidades. Ao menos sete especialidades (considere a afirmação de que “entre as especialidades há pediatria, clínica geral, gastrenterologia e dermatologia”).

```sql
insert into especialidade (codigo_especialidade, descricao_especialidade) values
(1, 'Cardiologia'),
(2, 'Pediatria'),
(3, 'Clínica geral'),
(4, 'Ortopedia'),
(5, 'Dermatologia'),
(6, 'Psiquiatria'),
(7, 'Ginecologia'),
(8, 'Oftalmologia'),
(9, 'Gastroenterologia'),
(10, 'Oncologia');

insert medico (codigo_medico, nome_medico, cpf_medico, rg_medico, crm_medico, cargo_medico, data_nasc_medico, codigo_especialidade) values
(1, 'Dr. João Silva', '123.456.789-00', 'MG1234567', 'CRM12345/MG', 'Cardiologista', '1975-04-15', 1),
(2, 'Dra. Maria Souza', '234.567.890-11', 'SP2345678', 'CRM23456/SP', 'Pediatra', '1980-06-20', 2),
(3, 'Dr. Carlos Pereira', '345.678.901-22', 'RJ3456789', 'CRM34567/RJ', 'Neurologista', '1978-09-10', 3),
(4, 'Dra. Ana Lima', '456.789.012-33', 'PR4567890', 'CRM45678/PR', 'Ortopedista', '1985-11-25', 4),
(5, 'Dr. Paulo Gomes', '567.890.123-44', 'RS5678901', 'CRM56789/RS', 'Dermatologista', '1970-12-30', 5),
(6, 'Dra. Fernanda Alves', '678.901.234-55', 'SC6789012', 'CRM67890/SC', 'Psiquiatra', '1982-03-18', 6),
(7, 'Dr. Luiz Martins', '789.012.345-66', 'BA7890123', 'CRM78901/BA', 'Ginecologista', '1973-07-22', 7),
(8, 'Dra. Helena Castro', '890.123.456-77', 'DF8901234', 'CRM89012/DF', 'Oftalmologista', '1988-05-14', 8),
(9, 'Dr. Ricardo Santos', '901.234.567-88', 'CE9012345', 'CRM90123/CE', 'Gastroenterologista', '1976-10-05', 9),
(10, 'Dra. Carolina Fernandes', '012.345.678-99', 'GO0123456', 'CRM01234/GO', 'Oncologista', '1981-08-19', 10);

insert into especialidade_medico (codigo_medico, codigo_especialidade) values
(1, 1), 
(2, 2), 
(3, 3), 
(4, 4), 
(5, 5), 
(6, 6), 
(7, 7), 
(8, 8), 
(9, 9), 
(10, 10), 
(1, 3), 
(2, 4), 
(3, 5), 
(4, 6), 
(5, 7), 
(6, 8), 
(7, 9), 
(8, 10), 
(9, 1), 
(10, 2); 
```

- Inclua ao menos 15 pacientes.
```sql
insert into convenio (numero_carteira, nome_convenio, tempo_carencia, cnpj_convenio) values
(1, 'Unimed', '30 dias', '11122233000101'),
(2, 'Amil', '60 dias', '22233344000202'),
(3, 'Bradesco Saúde', '45 dias', '33344455000303'),
(4, 'SulAmérica', '30 dias', '44455566000404'),
(5, 'Golden Cross', '60 dias', '55566677000505');

insert into paciente (codigo_paciente, nome_paciente, cpf_paciente, rg_paciente, telefone_paciente, email_paciente, data_nasc_paciente, numero_carteira_convenio) values
(1, 'Alice Souza', '12345678901', 'MG1234567', '31987654321', 'alice@gmail.com', '1990-01-19', 1),
(2, 'Bruno Lima', '23456789012', 'SP2345678', '11987654322', 'bruno@gmail.com', '1985-02-26', 2),
(3, 'Carlos Pereira', '34567890123', 'RJ3456789', '21987654323', 'carlos@gmail.com', '1995-03-30', 3),
(4, 'Daniela Santos', '45678901234', 'PR4567890', '41987654324', 'daniela@hotmail.com', '1980-04-15', 4),
(5, 'Eduardo Silva', '56789012345', 'RS5678901', '51987654325', 'eduardo@hotmail.com', '1975-12-05', 5),
(6, 'Fernanda Oliveira', '67890123456', 'SC6789012', '61987654326', 'fernanda@gmail.com', '1988-08-06', 1),
(7, 'Gabriel Costa', '78901234567', 'BA7890123', '71987654327', 'gabriel@gmail.com', '1979-05-07', 2),
(8, 'Helena Martins', '89012345678', 'DF8901234', '81987654328', 'helena@gmail.com', '1992-10-08', 3),
(9, 'Igor Almeida', '90123456789', 'CE9012345', '91987654329', 'igor@hotmail.com', '1983-09-04', 4),
(10, 'Julia Fernandes', '01234567890', 'GO0123456', '61987654330', 'julia@hotmail.com', '1991-10-17', 5),
(11, 'Lucas Rocha', '12345098765', 'MA1234509', '71987654331', 'lucas@gmail.com', '1987-12-11', 1),
(12, 'Mariana Ribeiro', '23456109876', 'PA2345610', '81987654332', 'mariana@hotmail.com', '1982-12-12', 2),
(13, 'Nicolas Lima', '34567210987', 'PE3456721', '91987654333', 'nicolas@gmail.com', '1993-01-13', 3),
(14, 'Olivia Silva', '45678321098', 'PI4567832', '61987654334', 'olivia@gmail.com', '1994-02-14', 4),
(15, 'Pedro Nunes', '56789432109', 'RJ5678943', '31987654335', 'pedro@hotmail.com', '1990-03-15', 5);

insert into endereco (codigo_endereco, rua, bairro, cep, numero, complemento, codigo_paciente) values
(1, 'Rua A', 'Bairro A', '30123456', 101, 'Apto 1', 1),
(2, 'Rua B', 'Bairro B', '40123456', 102, 'Apto 2', 2),
(3, 'Rua C', 'Bairro C', '50123456', 103, 'Apto 3', 3),
(4, 'Rua D', 'Bairro D', '60123456', 104, 'Apto 4', 4),
(5, 'Rua E', 'Bairro E', '70123456', 105, 'Apto 5', 5),
(6, 'Rua F', 'Bairro F', '80123456', 106, 'Apto 6', 6),
(7, 'Rua G', 'Bairro G', '90123456', 107, 'Apto 7', 7),
(8, 'Rua H', 'Bairro H', '01123456', 108, 'Apto 8', 8),
(9, 'Rua I', 'Bairro I', '11123456', 109, 'Apto 9', 9),
(10, 'Rua J', 'Bairro J', '12123456', 110, 'Apto 10', 10),
(11, 'Rua K', 'Bairro K', '13123456', 111, 'Apto 11', 11),
(12, 'Rua L', 'Bairro L', '14123456', 112, 'Apto 12', 12),
(13, 'Rua M', 'Bairro M', '15123456', 113, 'Apto 13', 13),
(14, 'Rua N', 'Bairro N', '16123456', 114, 'Apto 14', 14),
(15, 'Rua O', 'Bairro O', '17123456', 115, 'Apto 15', 15);
```
- Registre 20 consultas de diferentes pacientes e diferentes médicos (alguns pacientes realizam mais que uma consulta). As consultas devem ter ocorrido entre 01/01/2015 e 01/01/2022. Ao menos dez consultas devem ter receituário com dois ou mais medicamentos.

```sql
insert into consulta (codigo_consulta, data_consulta, horario_consulta, valor_consulta, forma_pagamento, codigo_paciente, codigo_medico, codigo_especialidade, numero_carteira_convenio) values
(1, '2015-01-15', '09:00:00', 150.00, 'Cartão', 1, 1, 1, 1),
(2, '2015-02-20', '10:30:00', 200.00, 'Dinheiro', 2, 2, 2, 2),
(3, '2016-03-25', '11:00:00', 175.00, 'Cartão', 3, 3, 3, 3),
(4, '2016-04-10', '08:45:00', 180.00, 'Cartão', 4, 4, 4, 4),
(5, '2017-05-05', '14:00:00', 160.00, 'Cartão', 5, 5, 5, 5),
(6, '2017-06-15', '15:30:00', 190.00, 'Cartão', 6, 6, 6, 1),
(7, '2018-07-20', '09:15:00', 170.00, 'Dinheiro', 7, 7, 7, 2),
(8, '2018-08-25', '10:00:00', 165.00, 'Cartão', 8, 8, 8, 3),
(9, '2019-09-30', '11:30:00', 185.00, 'Cartão', 9, 9, 9, 4),
(10, '2019-10-15', '13:00:00', 175.00, 'Dinheiro', 10, 10, 10, 5),
(11, '2020-01-10', '14:15:00', 200.00, 'Cartão', 11, 1, 1, 1),
(12, '2020-02-15', '15:45:00', 150.00, 'Dinheiro', 12, 2, 2, 2),
(13, '2020-03-20', '16:00:00', 170.00, 'Cartão', 13, 3, 3, 3),
(14, '2020-04-25', '17:30:00', 180.00, 'Cartão', 14, 4, 4, 4),
(15, '2021-05-30', '08:30:00', 160.00, 'Cartão', 15, 5, 5, 5),
(16, '2021-06-05', '09:45:00', 190.00, 'Cartão', 1, 6, 6, 1),
(17, '2021-07-10', '10:00:00', 165.00, 'Dinheiro', 2, 7, 7, 2),
(18, '2021-08-15', '11:15:00', 175.00, 'Cartão', 3, 8, 8, 3),
(19, '2021-09-20', '12:00:00', 185.00, 'Cartão', 4, 9, 9, 4),
(20, '2022-01-01', '13:45:00', 150.00, 'Dinheiro', 5, 10, 10, 5);

insert into receita (codigo_receita, nome_medicamento, qtd_medicamento, instrucoes_medicamento, codigo_consulta) values
(1, 'Paracetamol', 1, 'Tomar 1 comprimido a cada 8 horas', 1),
(2, 'Ibuprofeno', 2, 'Tomar 1 comprimido a cada 6 horas', 2),
(3, 'Amoxicilina', 4, 'Tomar 1 cápsula a cada 12 horas por 7 dias', 3),
(4, 'Losartana', 3, 'Tomar 1 comprimido ao dia', 4),
(5, 'Omeprazol', 1, 'Tomar 1 cápsula ao dia', 5),
(6, 'Metformina', 2, 'Tomar 1 comprimido 2 vezes ao dia', 6),
(7, 'Lorazepam', 1, 'Tomar 1 comprimido ao dormir', 7),
(8, 'Diclofenaco', 5, 'Tomar 1 comprimido a cada 8 horas', 8),
(9, 'Cetoconazol', 6, 'Aplicar o creme na área afetada 2 vezes ao dia', 9),
(10, 'Azitromicina', 2, 'Tomar 1 comprimido ao dia por 3 dias', 10),
(11, 'Atenolol', 2, 'Tomar 1 comprimido ao dia', 11),
(12, 'Prednisona', 1, 'Tomar 1 comprimido ao dia', 12),
(13, 'Aspirina', 8, 'Tomar 1 comprimido a cada 12 horas', 13),
(14, 'Clonazepam', 4, 'Tomar 1 comprimido ao dormir', 14),
(15, 'Sinvastatina', 4, 'Tomar 1 comprimido ao dia', 15),
(16, 'Nimesulida', 3, 'Tomar 1 comprimido a cada 8 horas', 16),
(17, 'Levotiroxina', 6, 'Tomar 1 comprimido ao dia', 17),
(18, 'Alprazolam', 3, 'Tomar 1 comprimido ao dormir', 18),
(19, 'Pantoprazol', 1, 'Tomar 1 comprimido ao dia', 19),
(20, 'Fluconazol', 1, 'Tomar 1 comprimido ao dia por 7 dias', 20);

insert into receita (codigo_receita, nome_medicamento, qtd_medicamento, instrucoes_medicamento, codigo_consulta) values
(21, 'Paracetamol', 1, 'Tomar 1 comprimido a cada 8 horas', 1),
(22, 'Ibuprofeno', 1, 'Tomar 1 comprimido a cada 6 horas', 2),
(23, 'Amoxicilina', 2, 'Tomar 1 cápsula a cada 12 horas por 7 dias', 3),
(24, 'Losartana', 4, 'Tomar 1 comprimido ao dia', 4),
(25, 'Omeprazol', 4, 'Tomar 1 cápsula ao dia', 5),
(26, 'Metformina', 3, 'Tomar 1 comprimido 2 vezes ao dia', 6),
(27, 'Lorazepam', 2, 'Tomar 1 comprimido ao dormir', 7),
(28, 'Diclofenaco', 9, 'Tomar 1 comprimido a cada 8 horas', 8),
(29, 'Cetoconazol', 8, 'Aplicar o creme na área afetada 2 vezes ao dia', 9),
(30, 'Azitromicina', 6, 'Tomar 1 comprimido ao dia por 3 dias', 10),
(31, 'Atenolol', 1, 'Tomar 1 comprimido ao dia', 11),
(32, 'Prednisona', 2, 'Tomar 1 comprimido ao dia', 12),
(33, 'Aspirina', 5, 'Tomar 1 comprimido a cada 12 horas', 13),
(34, 'Clonazepam', 5, 'Tomar 1 comprimido ao dormir', 14),
(35, 'Sinvastatina', 2, 'Tomar 1 comprimido ao dia', 15),
(36, 'Nimesulida', 2, 'Tomar 1 comprimido a cada 8 horas', 16),
(37, 'Levotiroxina', 1, 'Tomar 1 comprimido ao dia', 17),
(38, 'Alprazolam', 7, 'Tomar 1 comprimido ao dormir', 18),
(39, 'Pantoprazol', 7, 'Tomar 1 comprimido ao dia', 19),
(40, 'Fluconazol', 1,  'Tomar 1 comprimido ao dia por 7 dias', 20);

insert into consulta (codigo_consulta, data_consulta, horario_consulta, valor_consulta, forma_pagamento, codigo_paciente, codigo_medico, codigo_especialidade, numero_carteira_convenio) values
(21, '2022-02-01', '09:00:00', 150.00, 'Dinheiro', 1, 1, 1, NULL),
(22, '2022-02-10', '11:00:00', 200.00, 'Cartão', 2, 2, 2, NULL),
(23, '2022-03-01', '13:00:00', 175.00, 'Cartão', 3, 3, 3, NULL),
(24, '2022-03-15', '15:00:00', 180.00, 'Dinheiro', 4, 4, 4, NULL);

insert into receita (codigo_receita, nome_medicamento, qtd_medicamento, instrucoes_medicamento, codigo_consulta) values
(41, 'Dipirona', 1, 'Tomar 1 comprimido a cada 6 horas', 21),
(42, 'Vitamina C', 2, 'Tomar 1 comprimido ao dia', 22),
(43, 'Antialérgico', 1, 'Tomar 1 comprimido ao dia', 23),
(44, 'Ibuprofeno', 3, 'Tomar 1 comprimido a cada 8 horas', 24);
```

- Associe ao menos cinco pacientes a cinco consultas
```sql
insert into consulta (codigo_consulta, data_consulta, horario_consulta, valor_consulta, forma_pagamento, codigo_paciente, codigo_medico, codigo_especialidade, codigo_convenio) values
(1, '2020-01-15', '10:00:00', 200.00, 'Cartão de Crédito', 1, 1, 1, 1),
(2, '2019-03-20', '14:00:00', 150.00, 'Dinheiro', 2, 2, 2, 2),
(3, '2021-07-10', '09:30:00', 180.00, 'Cartão de Débito', 3, 3, 3, 3),
(4, '2018-05-25', '11:00:00', 220.00, 'Cheque', 4, 4, 4, 4),
(5, '2017-11-30', '16:00:00', 170.00, 'Dinheiro', 5, 5, 5, 5);
```

- Registre ao menos sete internações. Pelo menos dois pacientes devem ter se internado mais de uma vez. Ao menos três quartos devem ser cadastrados. As internações devem ter ocorrido entre 01/01/2015 e 01/01/2022. Considerando que “a princípio o hospital trabalha com apartamentos, quartos duplos e enfermaria”, inclua ao menos esses três tipos com valores diferentes. Inclua dados de dez profissionais de enfermaria. Associe cada internação a ao menos dois enfermeiros.
```sql
insert into tipo_quarto (codigo_tipo_quarto, diaria_quarto, descricao_quarto) values
(1, 300.00, 'Apartamento'),
(2, 150.00, 'Quarto Duplo'),
(3, 100.00, 'Enfermaria');

insert into quarto (numero_quarto, codigo_tipo_quarto) values
(101, 1),
(102, 2),
(103, 3);

insert into internacao (codigo_internacao, data_prevista_alta, data_entrada, data_alta, codigo_medico, numero_quarto, codigo_paciente, numero_carteira_convenio) values
(1, '2021-01-10', '2021-01-01', '2021-01-10', 1, 101, 1, 1),
(2, '2021-02-15', '2021-02-01', '2021-02-15', 2, 102, 2, 2),
(3, '2020-05-05', '2020-05-01', '2020-05-05', 3, 103, 3, 3),
(4, '2019-07-10', '2019-07-01', '2019-07-10', 4, 101, 4, 4),
(5, '2018-09-20', '2018-09-10', '2018-09-20', 5, 102, 5, 5),
(6, '2017-10-15', '2017-10-01', '2017-10-15', 6, 103, 1, 1),
(7, '2016-12-25', '2016-12-15', '2016-12-25', 7, 101, 2, 2);

insert into procedimento (codigo_procedimento, nome_procedimento, descricao_procedimento) values
(1, 'Cirurgia Cardíaca', 'Cirurgia para correção de problemas cardíacos'),
(2, 'Exame de Sangue', 'Coleta e análise de amostras de sangue'),
(3, 'Raio-X', 'Imagem radiográfica para diagnóstico'),
(4, 'Endoscopia', 'Exame do trato gastrointestinal'),
(5, 'Quimioterapia', 'Tratamento para câncer usando medicamentos');

insert into procedimento_internacao (codigo_internacao, codigo_procedimento) values
(1, 1),
(1, 2),
(2, 3),
(2, 4),
(3, 5),
(4, 1),
(5, 2),
(6, 3),
(7, 4);

insert into enfermeiro (codigo_enfermeiro, nome_enfermeiro, rg_enfermeiro, cpf_enfermeiro, cre_enfermeiro, data_nasc_enfermeiro) values
(1, 'Enf. João Costa', 'MG9876543', '33322211100', 'CRE12345/MG', '1985-01-01'),
(2, 'Enf. Maria Lima', 'SP8765432', '44433322211', 'CRE23456/SP', '1990-02-02'),
(3, 'Enf. Pedro Silva', 'RJ7654321', '55544433322', 'CRE34567/RJ', '1982-03-03'),
(4, 'Enf. Ana Santos', 'PR6543210', '66655544433', 'CRE45678/PR', '1975-04-04'),
(5, 'Enf. Carla Nunes', 'RS5432109', '77766655544', 'CRE56789/RS', '1983-05-05'),
(6, 'Enf. Bruno Souza', 'SC4321098', '88877766655', 'CRE67890/SC', '1991-06-06'),
(7, 'Enf. Paula Ribeiro', 'BA3210987', '99988877766', 'CRE78901/BA', '1974-07-07'),
(8, 'Enf. Luiz Martins', 'DF2109876', '11199988877', 'CRE89012/DF', '1987-08-08'),
(9, 'Enf. Fernanda Almeida', 'CE1098765', '22211199988', 'CRE90123/CE', '1976-09-09'),
(10, 'Enf. Ricardo Gonçalves', 'GO0987654', '33322211199', 'CRE01234/GO', '1992-10-10');

insert into enfermeiro_internacao (codigo_enfermeiro, codigo_internacao) values
(1, 1),
(2, 1),
(3, 2),
(4, 2),
(5, 3),
(6, 3),
(7, 4),
(8, 4),
(9, 5),
(10, 5),
(1, 6),
(2, 6),
(3, 7),
(4, 7);

insert into internacao (codigo_internacao, data_prevista_alta, data_entrada, data_alta, codigo_medico, numero_quarto, codigo_paciente, numero_carteira_convenio) values
(13, '2022-01-10', '2022-01-01', '2022-01-12', 1, 101, 1, 1),
(14, '2022-02-15', '2022-02-01', '2022-02-18', 2, 102, 2, 2),
(15, '2022-03-20', '2022-03-01', '2022-03-25', 3, 103, 3, 3),
(16, '2022-04-25', '2022-04-01', '2022-04-28', 4, 104, 4, 4);
```

# A Ordem do Alterar. 
Um banco de dados pode sofrer alterações ao longo da sua concepção e do seu desenvolvimento. Nesse momento devemos nos preparar para atualizar nossas estratégias. 
Pensando no banco que já foi criado para o Projeto do Hospital, realize algumas alterações nas tabelas e nos dados usando comandos de atualização e exclusão:
Crie um script que adicione uma coluna “em_atividade” para os médicos, indicando se ele ainda está atuando no hospital ou não. 
Crie um script para atualizar ao menos dois médicos como inativos e os demais em atividade.

```sql
alter table medico add column em_atividade varchar(10);

update medico
set em_atividade = "inativo"
where codigo_medico between 1 and 2;

update medico
set em_atividade = "ativo"
where codigo_medico between 3 and 10;

select * from medico;
```

# As Relíquias dos Dados
Uma vez que o banco estiver bem estruturado e desenhado, é possível realizar testes, simulando relatórios ou telas que o sistema possa necessitar. A tarefa consiste em criar consultas que levem aos resultados esperados.

- 1. Todos os dados e o valor médio das consultas do ano de 2020 e das que foram feitas sob convênio.
```sql
select * from consulta where year(data_consulta) = 2020 and numero_carteira_convenio is not null;
```

- 2. Todos os dados das internações que tiveram data de alta maior que a data prevista para a alta.
```sql
select * from internacao where data_alta > data_prevista_alta;
```

- 3. Receituário completo da primeira consulta registrada com receituário associado.
```sql
select * 
from receita as r
inner join consulta as c
on r.codigo_consulta = c.codigo_consulta
order by data_consulta asc
limit 1;
```

- 4. Todos os dados da consulta de maior valor e também da de menor valor (ambas as consultas não foram realizadas sob convênio).
```sql
select * from consulta where valor_consulta = (select max(valor_consulta) from consulta) or valor_consulta = (select min(valor_consulta) from consulta);
```

- 5. Todos os dados das internações em seus respectivos quartos, calculando o total da internação a partir do valor de diária do quarto e o número de dias entre a entrada e a alta.
```sql
select i.data_prevista_alta, i.data_entrada, i.data_alta, q.numero_quarto, tq.descricao_quarto, tq.diaria_quarto * datediff(i.data_alta, i.data_entrada) as total_internacao
from internacao as i
inner join quarto as q
on i.numero_quarto = q.numero_quarto
inner join tipo_quarto as tq
on q.codigo_tipo_quarto = tq.codigo_tipo_quarto;
```

- 6. Data, procedimento e número de quarto de internações em quartos do tipo “apartamento”.
```sql
select i.data_entrada, p.descricao_procedimento, q.numero_quarto, tq.descricao_quarto
from internacao as i
inner join procedimento_internacao ip
on ip.codigo_internacao = i.codigo_internacao
inner join procedimento p
on ip.codigo_procedimento = p.codigo_procedimento
inner join quarto as q
on i.numero_quarto = q.numero_quarto
inner join tipo_quarto as tq
on tq.codigo_tipo_quarto = q.codigo_tipo_quarto
where tq.descricao_quarto = 'Apartamento';
```

- 7. Nome do paciente, data da consulta e especialidade de todas as consultas em que os pacientes eram menores de 18 anos na data da consulta e cuja especialidade não seja “pediatria”, ordenando por data de realização da consulta.
```sql
select p.nome_paciente, c.data_consulta, e.descricao_especialidade
from paciente p
inner join consulta c
on p.codigo_paciente = c.codigo_paciente
inner join especialidade e 
on c.codigo_especialidade = e.codigo_especialidade
where (cast((select datediff(c.data_consulta, p.data_nasc_paciente)/365) as unsigned)) < 18 and e.descricao_especialidade != "Pediatra"
order by c.data_consulta;
```
 
- 8. Nome do paciente, nome do médico, data da internação e procedimentos das internações realizadas por médicos da especialidade “gastroenterologia”, que tenham acontecido em “enfermaria”.
```sql
select i.codigo_internacao, p.nome_paciente, m.nome_medico, i.data_entrada, po.descricao_procedimento
from paciente p
inner join internacao i
on p.codigo_paciente = i.codigo_paciente 
inner join medico m 
on m.codigo_medico = i.codigo_medico
inner join especialidade_medico me
on me.codigo_medico = m.codigo_medico
inner join especialidade e
on me.codigo_especialidade = e.codigo_especialidade
inner join procedimento_internacao pi
on pi.codigo_internacao = i.codigo_internacao
inner join procedimento po
on po.codigo_procedimento = pi.codigo_procedimento
inner join quarto q
on i.numero_quarto = q.numero_quarto
inner join tipo_quarto tq
on tq.codigo_tipo_quarto = q.codigo_tipo_quarto
where e.descricao_especialidade = 'Gastroenterologia' and tq.descricao_quarto = 'Enfermaria';
```

- 9. Os nomes dos médicos, seus CRMs e a quantidade de consultas que cada um realizou.
```sql
select nome_medico, crm_medico, count(codigo_consulta) as numero_consultas
from medico as m
inner join consulta as c on m.codigo_medico = c.codigo_medico group by nome_medico, crm_medico;
```

- 10. Todos os médicos que tenham "Gabriel" no nome.
```sql
select * from medico where nome_medico = 'Gabriel';
```

- 11. Os nomes, CREs e número de internações de enfermeiros que participaram de mais de uma internação.
```sql
select nome_enfermeiro, cre_enfermeiro, count(i.codigo_internacao) as internacoes
from enfermeiro as e
inner join enfermeiro_internacao as ei
on e.codigo_enfermeiro = ei.codigo_enfermeiro
inner join internacao as i 
on i.codigo_internacao = ei.codigo_internacao
group by nome_enfermeiro, cre_enfermeiro;
```
    
