-- Cria o banco de dados Oficina e seleciona-o para uso
CREATE DATABASE Oficina; 
USE Oficina;

-- Tabela Cliente para armazenar as informações dos clientes da oficina
CREATE TABLE Cliente (
    idCliente INT AUTO_INCREMENT, -- Identificador único para cada cliente
    nomeCompleto VARCHAR(45) NOT NULL, -- Nome do cliente
    CPF CHAR(11) NOT NULL, -- CPF do cliente
    telefone CHAR(20) NOT NULL, -- Telefone para contato
    email VARCHAR(45) NOT NULL, -- Email do cliente
    endereco VARCHAR(45) NOT NULL, -- Endereço do cliente
    PRIMARY KEY(idCliente) -- Define idCliente como chave primária
);

-- Tabela Veiculo para armazenar os dados dos veículos dos clientes
CREATE TABLE Veiculo (
    idVeiculo INT AUTO_INCREMENT, -- Identificador único para cada veículo
    idCliente INT NOT NULL, -- Relaciona o veículo a um cliente
    modelo VARCHAR(45) NOT NULL, -- Modelo do veículo
    marca VARCHAR(45) NOT NULL, -- Marca do veículo
    cor VARCHAR(45) NOT NULL, -- Marca do veículo
    ano CHAR(0) NOT NULL, -- Ano de fabricação do veículo
    placa VARCHAR(7) NOT NULL, -- Placa do veículo
    PRIMARY KEY (idVeiculo), -- Define idVeiculo como chave primária
    FOREIGN KEY (idCliente) REFERENCES Cliente(idCliente) -- Cria chave estrangeira para Cliente
);

-- Tabela Peca para armazenar os dados das peças disponíveis na oficina
CREATE TABLE Peca (
    idPeca INT AUTO_INCREMENT, -- Identificador único para cada peça
    marca VARCHAR(45) NOT NULL, -- Marca da peça
    modelo VARCHAR(45) NOT NULL, -- Modelo da peça
    valor DECIMAL(7.2) NOT NULL, -- Valor da peça (formato decimal com 2 casas decimais)
    PRIMARY KEY (idPeca) -- Define idPeca como chave primária
);

-- Tabela Especialidade para definir as especialidades dos serviços oferecidos
CREATE TABLE Especialidade (
    idEspecialidade INT AUTO_INCREMENT, -- Identificador único para cada especialidade
    especialidade VARCHAR(45) NOT NULL, -- Descrição da especialidade
    PRIMARY KEY (idEspecialidade) -- Define idEspecialidade como chave primária
);

-- Tabela Mecanico para armazenar os dados dos mecânicos da oficina
CREATE TABLE Mecanico (
    idMecanico INT AUTO_INCREMENT, -- Identificador único para cada mecânico
    nomeCompleto VARCHAR(45) NOT NULL, -- Nome do mecânico
    dataDeAdmissão DATE NOT NULL, -- Data de admissão do mecânico
	especialidade VARCHAR(45) NOT NULL, -- Especialidade do mecânico
    turnoDeTrabalho VARCHAR(45) NOT NULL, -- Turno de trabalho do mecânico
    telefone CHAR(20) NOT NULL, -- Telefone para contato
    endereco VARCHAR(100) NOT NULL, -- Endereço do mecânico
    PRIMARY KEY (idMecanico) -- Define idMecanico como chave primária
);

-- Tabela Mecanico_has_Especialidade para relacionar mecânicos com especialidades
CREATE TABLE Mecanico_has_Especialidade (
    idMecanico INT NOT NULL, -- Relaciona a um mecânico
    idEspecialidade INT NOT NULL, -- Relaciona a uma especialidade
    PRIMARY KEY (idMecanico, idEspecialidade), -- Define combinação como chave primária
    FOREIGN KEY (idMecanico) REFERENCES Mecanico(idMecanico), -- Chave estrangeira para Mecanico
    FOREIGN KEY (idEspecialidade) REFERENCES Especialidade(idEspecialidade) -- Chave estrangeira para Especialidade
);

-- Tabela OrdemServico para registrar os serviços realizados na oficina
CREATE TABLE OrdemServico (
    idOrdemServico INT AUTO_INCREMENT, -- Identificador único para cada ordem de serviço
    idCliente INT NOT NULL, -- Relaciona a ordem de serviço a um cliente
    idVeiculo INT NOT NULL, -- Relaciona a ordem de serviço a um veículo
    idMecanico INT NOT NULL, -- Relaciona a ordem de serviço a um mecânico
    idPeca INT, -- (Opcional) Relaciona a uma peça específica usada no serviço
    idEspecialidade INT NOT NULL, -- Relaciona a ordem de serviço a uma especialidade
    descricao VARCHAR(100) NOT NULL, -- Descrição do serviço realizado
    dataDeEmissão DATE NOT NULL, -- Data de início do serviço
    prazoEntrega DATE, -- Data de término do serviço (pode ser nulo se ainda estiver em andamento)
    valorTotal DECIMAL(10.2) NOT NULL, -- Valor total do serviço
    PRIMARY KEY (idOrdemServico), -- Define idOrdemServico como chave primária
    FOREIGN KEY (idCliente) REFERENCES Cliente(idCliente), -- Chave estrangeira para Cliente
    FOREIGN KEY (idVeiculo) REFERENCES Veiculo(idVeiculo), -- Chave estrangeira para Veiculo
    FOREIGN KEY (idMecanico) REFERENCES Mecanico(idMecanico), -- Chave estrangeira para Mecanico
    FOREIGN KEY (idPeca) REFERENCES Peca(idPeca), -- Chave estrangeira para Peca
    FOREIGN KEY (idEspecialidade) REFERENCES Especialidade(idEspecialidade) -- Chave estrangeira para Especialidade
);

ALTER TABLE Veiculo MODIFY COLUMN ano CHAR(4) NOT NULL;
ALTER TABLE Peca MODIFY COLUMN valor DECIMAL(10,2) NOT NULL;

INSERT INTO Cliente (nomeCompleto, CPF, telefone, email, endereco) VALUES 
('João Silva', '12345678901', '559199990000', 'joao.silva@gmail.com', 'Rua das Flores, 123'),
('Maria Oliveira', '98765432109', '559188880000', 'maria.oliveira@gmail.com', 'Av. Central, 456'),
('Carlos Pereira', '45678912345', '559177770000', 'carlos.pereira@yahoo.com', 'Travessa Verde, 789'),
('Ana Souza', '32165498721', '559166660000', 'ana.souza@hotmail.com', 'Praça Azul, 321'),
('Marcos Costa', '78912345678', '559155550000', 'marcos.costa@gmail.com', 'Vila Nova, 654'),
('Fernanda Santos', '65498732165', '559144440000', 'fernanda.santos@gmail.com', 'Beco Alegre, 987'),
('Rafael Lima', '15935724680', '559133330000', 'rafael.lima@gmail.com', 'Rua das Palmeiras, 147'),
('Bruna Almeida', '85274196352', '559122220000', 'bruna.almeida@gmail.com', 'Largo Bonito, 258'),
('Gabriel Ferreira', '96325874184', '559111110000', 'gabriel.ferreira@gmail.com', 'Passagem Nova, 369'),
('Larissa Martins', '74185296347', '559100000000', 'larissa.martins@gmail.com', 'Estação Central, 741'),
('Juliana Araújo', '12312312312', '559199990001', 'juliana.araujo@gmail.com', 'Estrada do Sol, 852'),
('Pedro Moreira', '32132132132', '559188880001', 'pedro.moreira@gmail.com', 'Alameda Viva, 963'),
('Lucas Gonçalves', '45645645645', '559177770001', 'lucas.goncalves@gmail.com', 'Jardim Encantado, 147'),
('Patrícia Lima', '65465465465', '559166660001', 'patricia.lima@gmail.com', 'Bosque Sonoro, 258'),
('Roberto Carvalho', '78978978978', '559155550001', 'roberto.carvalho@gmail.com', 'Serra Feliz, 369'),
('Vanessa Ribeiro', '98798798798', '559144440001', 'vanessa.ribeiro@gmail.com', 'Ponte Alta, 741'),
('André Vieira', '85285285285', '559133330001', 'andre.vieira@gmail.com', 'Travessa Calma, 852'),
('Simone Mendes', '15915915915', '559122220001', 'simone.mendes@gmail.com', 'Rua Longa, 963'),
('Diego Lopes', '75375375375', '559111110001', 'diego.lopes@gmail.com', 'Estrada Bela, 147'),
('Carla Rocha', '95195195195', '559100000001', 'carla.rocha@gmail.com', 'Praça Alegre, 258');

INSERT INTO Veiculo (idCliente, modelo, marca, cor, ano, placa) VALUES 
(1, 'Civic', 'Honda', 'Preto', '2020', 'ABC1234'),
(2, 'Corolla', 'Toyota', 'Branco', '2019', 'DEF5678'),
(3, 'Gol', 'Volkswagen', 'Vermelho', '2018', 'GHI9101'),
(4, 'HB20', 'Hyundai', 'Azul', '2021', 'JKL1213'),
(5, 'Onix', 'Chevrolet', 'Cinza', '2022', 'MNO1415'),
(6, 'Cruze', 'Chevrolet', 'Prata', '2017', 'PQR1617'),
(7, 'Fiesta', 'Ford', 'Preto', '2016', 'STU1819'),
(8, 'EcoSport', 'Ford', 'Branco', '2020', 'VWX2021'),
(9, 'Palio', 'Fiat', 'Vermelho', '2015', 'YZA2223'),
(10, 'Uno', 'Fiat', 'Verde', '2014', 'BCD2425'),
(11, 'Renegade', 'Jeep', 'Preto', '2023', 'EFG2627'),
(12, 'Compass', 'Jeep', 'Azul', '2022', 'HIJ2829'),
(13, 'Civic', 'Honda', 'Branco', '2020', 'KLM3031'),
(14, 'Accord', 'Honda', 'Cinza', '2021', 'NOP3233'),
(15, 'Corolla Cross', 'Toyota', 'Prata', '2023', 'QRS3435'),
(16, 'Hilux', 'Toyota', 'Preto', '2021', 'TUV3637'),
(17, 'Golf', 'Volkswagen', 'Vermelho', '2019', 'WXY3839'),
(18, 'Polo', 'Volkswagen', 'Azul', '2020', 'ZAB4041'),
(19, 'Siena', 'Fiat', 'Cinza', '2017', 'CDE4243'),
(20, 'Toro', 'Fiat', 'Branco', '2023', 'FGH4445');

INSERT INTO Peca (marca, modelo, valor) VALUES
('Bosch', 'Filtro de Ar', 45.90),
('NGK', 'Velas de Ignição', 120.50),
('Pirelli', 'Pneu 195/60', 350.00),
('Mobil', 'Óleo 5W30', 80.20),
('Fram', 'Filtro de Óleo', 35.70),
('Monroe', 'Amortecedor', 450.00),
('Valeo', 'Pastilhas de Freio', 220.90),
('Bosch', 'Bateria 60Ah', 450.00),
('Continental', 'Correia Dentada', 80.00),
('Hella', 'Farol Principal', 520.00),
('Magneti Marelli', 'Bomba de Combustível', 250.00),
('Valeo', 'Disco de Freio', 190.50),
('KYB', 'Molas de Suspensão', 300.00),
('Denso', 'Sensor de Temperatura', 120.00),
('Mahle', 'Filtro de Combustível', 30.90),
('Bosch', 'Alternador', 750.00),
('Pirelli', 'Pneu 205/55', 400.00),
('Fram', 'Filtro de Cabine', 55.00),
('NGK', 'Bobina de Ignição', 210.70),
('Philips', 'Lâmpada Halógena', 60.50);

INSERT INTO Especialidade (especialidade) VALUES
('Mecânico Geral'),
('Suspensão e Direção'),
('Elétrica Automotiva'),
('Manutenção de Freios'),
('Troca de Óleo'),
('Revisão de Motor'),
('Diagnóstico e Reparos'),
('Manutenção Preventiva'),
('Instalação de Acessórios'),
('Revisão de Ar-Condicionado'),
('Alinhamento e Balanceamento'),
('Reparo de Pneus'),
('Programação Eletrônica'),
('Manutenção de Transmissão'),
('Higienização Interna'),
('Reparo de Carroceria'),
('Soldagem Automotiva'),
('Montagem de Peças'),
('Serviços de Escapamento'),
('Serviços de Pintura Automotiva');

INSERT INTO Mecanico (nomeCompleto, dataDeAdmissão, especialidade, turnoDeTrabalho, telefone, endereco) VALUES
('Carlos Silva', '2022-01-15', 'Elétrica Automotiva', 'Diurno', '559199990000', 'Rua das Flores, 123'),
('Ana Santos', '2021-08-10', 'Suspensão e Direção', 'Noturno', '559188880000', 'Av. Central, 456'),
('Pedro Oliveira', '2023-03-20', 'Manutenção de Freios', 'Diurno', '559177770000', 'Travessa Verde, 789'),
('Juliana Costa', '2020-11-05', 'Troca de Óleo', 'Diurno', '559166660000', 'Praça Azul, 321'),
('Rafael Lima', '2019-06-25', 'Revisão de Motor', 'Diurno', '559155550000', 'Vila Nova, 654'),
('Fernanda Almeida', '2022-02-14', 'Manutenção Preventiva', 'Noturno', '559144440000', 'Beco Alegre, 987'),
('Lucas Martins', '2021-07-01', 'Diagnóstico e Reparos', 'Diurno', '559133330000', 'Rua das Palmeiras, 147'),
('Bruna Ferreira', '2023-01-10', 'Revisão de Ar-Condicionado', 'Noturno', '559122220000', 'Largo Bonito, 258'),
('Gabriel Lopes', '2020-05-19', 'Alinhamento e Balanceamento', 'Diurno', '559111110000', 'Passagem Nova, 369'),
('Larissa Mendes', '2019-12-12', 'Reparo de Pneus', 'Noturno', '559100000000', 'Estação Central, 741'),
('Roberto Carvalho', '2023-04-01', 'Programação Eletrônica', 'Diurno', '559199990001', 'Estrada do Sol, 852'),
('Vanessa Ribeiro', '2022-11-15', 'Manutenção de Transmissão', 'Noturno', '559188880001', 'Alameda Viva, 963'),
('André Vieira', '2021-09-30', 'Higienização Interna', 'Diurno', '559177770001', 'Jardim Encantado, 147'),
('Simone Mendes', '2020-03-08', 'Reparo de Carroceria', 'Diurno', '559166660001', 'Bosque Sonoro, 258'),
('Diego Moreira', '2022-06-18', 'Soldagem Automotiva', 'Noturno', '559155550001', 'Serra Feliz, 369'),
('Carla Rocha', '2023-05-03', 'Montagem de Peças', 'Diurno', '559144440001', 'Ponte Alta, 741'),
('João Moreira', '2021-04-25', 'Serviços de Escapamento', 'Diurno', '559133330001', 'Travessa Calma, 852'),
('Maria Gonçalves', '2019-02-10', 'Serviços de Pintura Automotiva', 'Noturno', '559122220001', 'Rua Longa, 963'),
('Paulo Lima', '2023-03-15', 'Elétrica Automotiva', 'Diurno', '559111110001', 'Estrada Bela, 147'),
('Patrícia Araújo', '2022-12-20', 'Revisão de Motor', 'Noturno', '559100000001', 'Praça Alegre, 258');

INSERT INTO Mecanico_has_Especialidade (idMecanico, idEspecialidade) VALUES
(1, 3),
(2, 2),
(3, 4),
(4, 5),
(5, 6),
(6, 7),
(7, 8),
(8, 10),
(9, 11),
(10, 12),
(11, 13),
(12, 14),
(13, 15),
(14, 16),
(15, 17),
(16, 18),
(17, 19),
(18, 20),
(19, 3),
(20, 6);

INSERT INTO OrdemServico (idCliente, idVeiculo, idMecanico, idPeca, idEspecialidade, descricao, dataDeEmissão, prazoEntrega, valorTotal) VALUES
(1, 1, 1, 1, 3, 'Substituição de filtro de ar', '2025-03-15', '2025-03-17', 150.00),
(2, 2, 2, 2, 2, 'Troca de velas de ignição', '2025-03-16', '2025-03-18', 200.00),
(3, 3, 3, 3, 4, 'Substituição de pneus dianteiros', '2025-03-17', '2025-03-19', 700.00),
(4, 4, 4, 4, 5, 'Troca de óleo e filtro', '2025-03-18', '2025-03-19', 130.00),
(5, 5, 5, 5, 6, 'Revisão completa do motor', '2025-03-19', '2025-03-25', 900.00),
(6, 6, 6, 6, 7, 'Inspeção de freios e troca de pastilhas', '2025-03-20', '2025-03-22', 250.00),
(7, 7, 7, 7, 8, 'Manutenção preventiva com alinhamento', '2025-03-21', '2025-03-23', 300.00),
(8, 8, 8, 8, 10, 'Instalação de ar-condicionado', '2025-03-22', '2025-03-26', 1500.00),
(9, 9, 9, 9, 11, 'Balanceamento de rodas', '2025-03-23', '2025-03-23', 80.00),
(10, 10, 10, 10, 12, 'Reparo de pneu traseiro', '2025-03-24', '2025-03-24', 50.00),
(11, 11, 11, 11, 13, 'Reprogramação eletrônica do motor', '2025-03-25', '2025-03-26', 500.00),
(12, 12, 12, 12, 14, 'Revisão da transmissão', '2025-03-26', '2025-03-28', 600.00),
(13, 13, 13, 13, 15, 'Limpeza interna completa', '2025-03-27', '2025-03-27', 150.00),
(14, 14, 14, 14, 16, 'Reparo na carroceria', '2025-03-28', '2025-03-30', 1200.00),
(15, 15, 15, 15, 17, 'Soldagem de escapamento', '2025-03-29', '2025-03-30', 300.00),
(16, 16, 16, 16, 18, 'Montagem de peças de suspensão', '2025-03-30', '2025-04-01', 400.00),
(17, 17, 17, 17, 19, 'Reparo no sistema de escape', '2025-03-31', '2025-04-01', 350.00),
(18, 18, 18, 18, 20, 'Pintura da lateral direita', '2025-04-01', '2025-04-05', 2000.00),
(19, 19, 19, 19, 3, 'Substituição de alternador', '2025-04-02', '2025-04-03', 800.00),
(20, 20, 20, 20, 6, 'Revisão geral com diagnóstico', '2025-04-03', '2025-04-06', 1200.00);

-- 1. Recuperar todos os dados dos clientes cadastrados
SELECT * FROM Cliente;

-- 2. Selecionar veículos fabricados a partir de 2020
SELECT modelo, marca, ano 
FROM Veiculo 
WHERE ano >= '2020';

-- 3. Calcular o lucro estimado de cada ordem de serviço (valorTotal menos o valor da peça utilizada)
SELECT idOrdemServico, descricao, valorTotal - COALESCE((SELECT valor FROM Peca WHERE Peca.idPeca = OrdemServico.idPeca), 0) AS lucroEstimado 
FROM OrdemServico;

-- 4. Listar os clientes ordenados alfabeticamente pelo nome completo
SELECT nomeCompleto, telefone, email 
FROM Cliente 
ORDER BY nomeCompleto ASC;

-- 5. Listar especialidades com mais de 2 mecânicos associados
SELECT e.especialidade, COUNT(mhe.idMecanico) AS totalMecanicos
FROM Especialidade e
JOIN Mecanico_has_Especialidade mhe ON e.idEspecialidade = mhe.idEspecialidade
GROUP BY e.especialidade
HAVING COUNT(mhe.idMecanico) > 2;

-- 6. Obter os dados de ordens de serviço com nomes dos clientes e modelos dos veículos
SELECT os.idOrdemServico, c.nomeCompleto, v.modelo, os.descricao, os.valorTotal
FROM OrdemServico os
JOIN Cliente c ON os.idCliente = c.idCliente
JOIN Veiculo v ON os.idVeiculo = v.idVeiculo;

-- 7. Selecionar ordens de serviço cujo prazo de entrega seja posterior à data atual
SELECT os.idOrdemServico, os.descricao, os.prazoEntrega
FROM OrdemServico os
WHERE os.prazoEntrega > CURDATE();

-- 8. Agrupar veículos registrados para cada cliente
SELECT c.nomeCompleto, COUNT(v.idVeiculo) AS totalVeiculos
FROM Cliente c
LEFT JOIN Veiculo v ON c.idCliente = v.idCliente
GROUP BY c.nomeCompleto
ORDER BY totalVeiculos DESC;

-- 9. Obter os mecânicos e suas especialidades
SELECT m.nomeCompleto, e.especialidade
FROM Mecanico m
JOIN Mecanico_has_Especialidade mhe ON m.idMecanico = mhe.idMecanico
JOIN Especialidade e ON mhe.idEspecialidade = e.idEspecialidade
ORDER BY m.nomeCompleto;

-- 10. Exibir o custo médio das ordens de serviço por especialidade
SELECT e.especialidade, AVG(os.valorTotal) AS custoMedio
FROM OrdemServico os
JOIN Especialidade e ON os.idEspecialidade = e.idEspecialidade
GROUP BY e.especialidade
HAVING AVG(os.valorTotal) > 100;

INSERT INTO Mecanico_has_Especialidade (idMecanico, idEspecialidade) VALUES
(1, 2), -- Adicionando uma segunda especialidade ao Mecânico 1
(2, 3), -- Adicionando uma segunda especialidade ao Mecânico 2
(3, 5), -- Adicionando uma segunda especialidade ao Mecânico 3
(4, 6), -- Adicionando uma segunda especialidade ao Mecânico 4
(5, 7), -- Adicionando uma segunda especialidade ao Mecânico 5
(6, 10), -- Adicionando uma segunda especialidade ao Mecânico 6
(7, 11), -- Adicionando uma segunda especialidade ao Mecânico 7
(8, 8), -- Adicionando uma segunda especialidade ao Mecânico 8
(9, 13), -- Adicionando uma segunda especialidade ao Mecânico 9
(10, 15); -- Adicionando uma segunda especialidade ao Mecânico 10
