#PROCEDURES
##EX1
~~~mysql

~~~
##EX2
~~~mysql
DELIMITER //
DROP PROCEDURE IF EXISTS spIntercanvi //
CREATE PROCEDURE spIntercanvi(IN pEmpleat_id1 INT, IN pEmpleat_id2 INT)
BEGIN
    DECLARE vSalari DECIMAL (8,2);
    -- Comprobar si existeix empleat
    IF(SELECT empleat_id
            FROM empleats
       WHERE empleat_id = pEmpleat_id1) IS NOT NULL
       AND SELECT empleat_id
            FROM empleats
       WHERE empleat_id = pEmpleat_id2) IS NOT NULL
       THEN
    -- Intercanviar salaris
       SELECT salari INTO vSalari
            FROM emplets 
            
       
~~~
##EX3
~~~mysql
DELIMITER //
DROP PROCEDURE IF EXISTS spIntercanvi //
CREATE PROCEDURE spIntercanvi(IN pEmpleat_id1 INT, IN pEmpleat_id2 INT)
BEGIN
    -- Comprovar si els empleats existeixen
    IF spExisteixEmpleat (pEmpleat_id1) = 1
        AND spExisteixEmpleat (pEmpleat_id2) = 1 THEN
    -- Obtenir departament_id de pEmpleat_id1
    
    -- Modificar departament_id de pEmpleat_id2
       UPDATE empleats
            departament_id = (SELECT epartament_id
                                    FROM empleats
                              WHERE empleat_id = pEmpleat_id1;
    
END;
//                            
~~~
##EX4
~~~mysql
DELIMITER //
DROP PROCEDURE IF EXISTS spMoureEmpleats //
CREATE PROCEDURE spMoureEmpleats(IN pDep_Id1 INT, IN pDep_Id2 INT)
BEGIN
    UPDATE empleats
        SET departament_id = pDep_Id1
    WHERE departament_id = pDep_id2;
END;
//
~~~
##EX5
~~~mysql
DELIMITER //
DROP PROCEDURE IF EXISTS spMostrarEmpleats //
CREATE PROCEDURE spMostrarEmpleats()
BEGIN
    SELECT e.empleat_id, e.nom AS nom_empleat, d.nom AS nom_departament, l.ciutat
        FROM empleats e
        INNER JOIN departament d ON d.departament_id = e.departament_id
        INNER JOIN localitzacions l ON l.localitzacio_id = d.localitzacio_id;
END;
//
~~~
##EX6
~~~mysql
DELIMITER //
DROP PROCEDURE IF EXISTS spInfoEmpleats //
CREATE PROCEDURE spInfoEmpleats()
BEGIN
    SELECT *
        FORM empleats;
END;
//
~~~
##EX7
~~~mysql
DELIMITER //
DROP PROCEDURE IF EXISTS spRegistro //
CREATE PROCEDURE spRegistro(IN pEmpleat_id INT)
BEGIN
    CREATE TABLE IF NOT EXISTS registres
    (
    empleat_id      TINYINT,
    sesio           DATETIME,
    CONSTRAINT pk_registre PRIMARY KEY (empleat_id, sesio);
    );
    INSERT INTO registres SELECT (empleat_id, sesio) VALUE(pEmpleat_id, CONCAT(CURDATE(), NOW()));
    
END;
//
~~~