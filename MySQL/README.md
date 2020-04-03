# Instalación MySQL
1. Imos a [https://dev.mysql.com/downloads/windows/installer/8.0.html](https://dev.mysql.com/downloads/windows/installer/8.0.html) e descargamos o instalador de MySQL.
2. Unha vez descargado instalámolo, executando o .msi .
3. En "Choosing a setup type" eleximos Developer Default, que instalará automáticamente todo o necesario para poder crear e modificar bases de datos.
""mysql1""
4. Continuamos dándolle a next, neste paso poderemos comprobar os productos que se instalarán.
""mysql2"
5. Unha vez que termine de instalarse todo correctamente dámoslle a next.
""mysql3"
6. En Group Replication seleccionamos Standalone MySQL Server/Classic MySQL Replication.
7. En Authentication Method seleccionamos Use Strong Password Encryption...
8. Agora deberemos especificar unha contraseña e añadir un usuario, dámoslle a next o terminar.
""mysql4""
9. En Windows Service deixamos todo como está ou si queremos cambiámoslle o nome a Windows Service Name, dámoslle a next.
10. Dámoslle a Execute para executar os cambios, cando termine dámoslle a Finish.
""mysql5"
11. En Connect to Server, abaixo deberemos por a contraseña que introducimos anteriormente, unha vez posta, dámoslle a check e mostrarásenos a seguinte mensaxe.
""mysql6"
12. Cando rematemos, dámoslle a next e teranse que aplicar unhas novas configuracións, dámoslle a Execute.
""mysql7"
13. Cando remate aparecerá unha nova ventá, dámoslle a next.
14. A instalación estará completa, dámoslle a Finish.
""mysql8"
15. Agora podemos ir ao cmd a comprobar que temos mysql instalado, para eso escribimos `mysql --version`
16. É probable que nos salga o seguinte erro.
""mysql9"
17. Para arreglalo, imos a Program Files>MySQL>MySQL Server 8.0>bin e copiamos a dirección.
18. Buscamos no Inicio "variables de entorno" para poder acceder ao editor de variables de entorno do sistema.
""mysql10"
19. Seleccionamos Variables de Entorno.
20. Teremos que editar a variable PATH, e añadir a ruta que copiamos anteriormente onde se atopa o mySQL.
""mysql11"
21. Gardamos todo e cerramos o editor das variables de entorno.
22. Se volvemos ao cmd e repetimos o paso número 15 mostrarásenos a versión.
""mysql14"
23. Usamos `mysql -u root - p` donde root é o usuario, agora pediranos a contraseña, poñémola.
""mysql12"
""mysql13"
  
  
