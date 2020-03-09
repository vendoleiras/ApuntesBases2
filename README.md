# ApuntesBases2
> Añadidos despois de editalos aparte en StackEdit, están en sucio e faltan cousas obvio
### SUBLENGUAJES SQL
- DDL – Data Definition Language.
CREATE,ALTER,DROP,TRUNCATE,RENAME

- DML – Data Manipulation Language.
INSERT, UPDATE, DELETE 

- DRL/DQL – Data Retrieval Language/Data Query Language.
 SELECT

- TCL – Transaction Query Language /Transaction Control Language
COMMIT, ROLLBACK (volve atrás, si algo falla), SAVEPOINT (punto donde dices si ata eiqui non fallou nada esto enviamo e non o tires todo)

- DCL – Data Control Language.
GRANT(permitimos que este usuario faga esto),REVOKE(darlle marcha atrás) ,AUDIT,COMMENT, ANALYZE 

- SCL – Session Control Language.
ALTER SESSION,SET ROLL


### A ter en conta (Acciones referenciales)
>  CASCADE: Cando se fai  UPDATE/ DELETE na táboa pai, automaticamente actualizaranse/borrarán as filas relacionadas da táboa filla.
> SET  NULL: Cando se fai  UPDATE/ DELETE na táboa pai, as claves foráneas das filas relacionadas na táboa filla poñeranse A  NULL. É importante asegurarse que eses campos non terán a restrición de  NOT  NULL ou poderás recibir erros.
>  RESTRICT (ou NON  ACTION): se se tenta facer unha acción de  UPDATE/ DELETE na táboa pai esta será rexeitada automaticamente.
> SET  DEFAULT: Dás un valor por defecto á columna.

CONSTRAINTS
- NOT NULL
- PRIMARY KEY
- FOREIGN KEY
- CHECK
- DEFAULT
- CHECK (todos os valores da columna cumplan unha condición específica)
---
### DML
- INSERT


INSERT INTO <nome_da_táboa>
[(<atributo_1>,<atributo_2>,...)]
(VALUES(<valor_1>,<valor_2>,...)] | (SELECT...);
 
o select ten que ser: - co mesmo número de columnas, e cos mesmos dominios -> (tipos de datos (DATETIME, NCHAR, INTEGER))

exemplo---- (1,'cheese',9.99)
  
Ejemplo 1 (inserto valores alumno pepe en la materia spd2 a la tabla cursada):

INSERT INTO ''cursada'' (''alumno'', ''materia'') VALUES (''pepe'', ''spd2'')

- UPDATE

UPDATE <nome_da_táboa>
SET <atributo_1>=<valor_1>,

<atributo_2>=<valor_2>,

... (mais cousas)

[WHERE <p_redicado>];
  
Ejemplo:

UPDATE world

   SET name='España',
   
   continent= 'Africa'
   
   WHERE name= 'Spain';
   
- DELETE

DELETE FROM <nome_da_taboa>

[WHERE <p_redicado>];
  
Ejemplo:

DELETE FROM world

WHERE population > 100000000;

---

Numeros (pg)

- integer

- decimal (preciso)

- real (non preciso)

TEXTO pode ser 'char' | 'varchar' | 'text'

- char -> ten lonxitude fixa | char(10) un dni ten que ter tantos caracteres non é algo variable.

- varchar -> lonxitude variable | varchar(20) 

- text -> non podes por limite de tamaño, e ocupa moito espacio

---

TEMPO hai 'date' | 'time' | 'timestamp'

- date -> dia, mes, ano

- time -> hora, minutos, segundos... [zona_horaria]

- timestamp -> date + time

---

OTROS -> 'boolean' | 'money' | 'json' | 'cidr' | 'uuid' | 'inet'

- boolean -> true (1) | false (0) |||| NULL -> NOT NULL

- money -> para os dineros

- json -> actualmente usase esto, en bancos e administracion publica usase xml


---

CASCADE usase no 90% dos casos, as modificacións van ser casi siempre cascada
DEFAULT usábase hai moito tempo, agora apenas nada, é falsear información

---

Para crear un dominio
CREATE DOMAIN Tipo_DNI CHAR(9);
CREATE DOMAIN Tipo_Código CHAR(5);
CREATE DOMAIN Nome_Válido CHAR(30); Neste é mellor usar VARCHAR

Esto non é obligatorio usalo no exame pero é moito máis cómodo

---

CREATE TABLE Investigación.Sede (
	Nome_Sede Nome_Válido PRIMARY KEY,  >así non deberíamos por unha primary key
	Campus    Nome_Válido NOT NULL,
);

Facelo así mellor

CREATE TABLE Investigación.Sede (
	Nome_Sede Nome_Válido,
	Campus    Nome_Válido NOT NULL,
	CONSTRAINT PC_Sede
		PRIMARY KEY (Nome_Sede)
);

Si non leva asterisco tes que por NOT NULL

CREATE TABLE Investigación.Departamento (
	Nome_Departamento Nome_Válido PRIMARY KEY, --- si é simple podes por eiqui o PRIMARY KEY igual que no anterior
	Teléfono          CHAR(9) NOT NULL,
	Director          Tipo_DNI,
 
 Eiqui por exemplo non podrías por PRIMARY KEY en cada un, MOTIVO DE SUSPENSO
 
 CREATE TABLE Investigación.Ubicación (
	Nome_Sede		  Nome_Válido,
	Nome_Departamento Nome_Válido,
	PRIMARY KEY (Nome_Sede, Nome_Departamento)
 
 De cara ao exame é mellor usar ALTER TABLE pero miramos todos os exemplos
 
 CREATE TABLE Investigación.Ubicación (
	Nome_Sede		  Nome_Válido,
	Nome_Departamento Nome_Válido,
	PRIMARY KEY (Nome_Sede, Nome_Departamento),
	CONSTRAINT FK_Sede_Ubicación
		FOREIGN KEY (Nome_Sede)
		  REFERENCES Investigación.Sede (Nome_Sede)
		  ON DELETE CASCADE
		  ON UPDATE CASCADE,
	CONSTRAINT FK_Departamento_Ubicación
		FOREIGN KEY (Nome_Departamento)
		  REFERENCES Investigación.Departamento (Nome_Departamento)
		  ON DELETE CASCADE
		  ON UPDATE CASCADE
);

CREATE TABLE Investigacion.Grupo (
	Nome_Grupo         Nome_Válido,
	Nome_Departamento  Nome_Válido,
	Área			   Nome_Válido NOT NULL,
	Lider			   Tipo_DNI,
	PRIMARY KEY (Nome_Grupo, Nome_Departamento),
	FOREIGN KEY (Nome_Departamento)
	  REFERENCES Investigación.Departamento (Nome_Departamento)
	  ON DELETE CASCADE
	  ON UPDATE CASCADE
	-- FK (Lider)
);

CREATE TABLE Investigación.Profesor (
	DNI            Tipo_DNI PRIMARY KEY,
	Nome_Profesor  Nome_Válido NOT NULL,
	Titulación     VARCHAR(29) NOT NULL,
	Experiencia    Integer,
	N_Grupo        Nome_Válido,
	N_Departamento Nome_Válido,
	FOREIGN KEY (N_Grupo, N_Departamento)
	  REFERENCES Investigación.Grupo (N_Grupo, N_Departamento)
	  ON DELETE SET NULL
	  ON UPDATE CASCADE
);

ALTER TABLE Investigacion.Departamento
	ADD CONSTRAINT FK_Profesor_Departamento
		FOREIGN KEY (Director)
			REFERENCES Profesor (DNI)
			ON DELETE SET NULL
				ON UPDATE CASCADE;
		
--- a foreign key de profesor tá mal . facer unha nova
--- foreign key con B:N M:R

ALTER TABLE Investigación.Profesor
	DROP CONSTRAINT FK_Grupo_Profesor;
	
ALTER TABLE Profesor
	ADD CONSTRAINT FK_Grupo_Profesor
	FOREIGN KEY (N_Grupo, N_Departamento)
		REFERENCES Grupo (Nome_Grupo, Nome_Departamento)
		ON DELETE SET NULL
		ON UPDATE NO ACTION;
	
