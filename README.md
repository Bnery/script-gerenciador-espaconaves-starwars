# script-gerenciador-espaconaves-starwars
Criando um gerenciador de espaçonaves do star wars com SQL Server

Neste desafio o expert cria um gerenciador de espaço naves do Star Wars modelando um banco de dados em SQL Server. Sua missão será entregar os scripts de criação das tabelas que compõem a estrutura desse banco de dados. Nesse sentido, você pode organizar esse repositório da forma como preferir... Dica: organizar tudo em seu README.md pode ser uma alternativa bem rápida e efetiva, principalmente porque o GitHub provê uma interface bem simples e intuitiva para isso. Bons estudos!

CREATE TABLE Naves(
	IdNave INT NOT NULL,
	Nome VARCHAR(100) NOT NULL,
	Modelo VARCHAR(50) NOT NULL,
	Passageiros INT NOT NULL,
	Carga FLOAT NOT NULL,
	Classe VARCHAR(100) NOT NULL	
)

ALTER TABLE Naves ADD CONSTRAINT PK_Naves PRIMARY KEY (IdNave);

CREATE TABLE Pilotos(
	IdPiloto INT NOT NULL,
	Nome VARCHAR(200) NOT NULL,
	AnoNascimento VARCHAR(10),
	IdPlaneta INT NOT NULL
)

ALTER TABLE Pilotos ADD CONSTRAINT PK_Pilotos PRIMARY KEY (IdPiloto)
ALTER TABLE Pilotos ADD CONSTRAINT FK_Pilotos_Planetas FOREIGN KEY (IdPlaneta) REFERENCES Planetas (IdPlaneta)

CREATE TABLE PilotosNaves(
	IdPiloto INT NOT NULL,
	IdNave INT NOT NULL,
	FlagAutorizado BIT NOT NULL
)

ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto,IdNave)
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREIGN KEY (IdPiloto) REFERENCES Pilotos (IdPiloto)
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Naves FOREIGN KEY (IdNave) REFERENCES Naves (IdNave)
ALTER TABLE PilotosNaves ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado DEFAULT (1) FOR FlagAutorizado

CREATE TABLE HistoricoViagens(
	IdNave INT NOT NULL,
	IdPiloto INT NOT NULL,
	DtSaida DATETIME NOT NULL,
	DtChegada DATETIME NOT NULL
)

ALTER TABLE HistoricoViagens ADD CONSTRAINT FK_HistoricoViagens_PilotosNaves FOREIGN KEY (IdPiloto, IdNave) REFERENCES PilotosNaves (IdPiloto, IdNave)
ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves
