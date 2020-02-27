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
