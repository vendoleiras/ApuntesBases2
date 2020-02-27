# ApuntesBases2
> Añadidos despois de editalos aparte en StackEdit, están en sucio e faltan cousas obvio
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
