#PROCEDURES
##EX1
~~~mysql
DELIMITER //

DROP FUNCTION IF EXISTS spData //
CREATE FUNCTION spData(pData DATE) 
RETURNS CHAR (10) DETERMINISTIC
BEGIN
    DECLARE vReturn CHAR(10);
	SET vReturn = DATE_FORMAT(pData, "%d-%m-%Y");
	RETURN vReturn;
END
//
DELIMITER ;DELIMITER //

DROP FUNCTION IF EXISTS spData //
CREATE FUNCTION spData(pData DATE) 
RETURNS CHAR (10) DETERMINISTIC
BEGIN
    DECLARE vReturn CHAR(10);
	SET vReturn = DATE_FORMAT(pData, "%d-%m-%Y");
	RETURN vReturn;
END
//
DELIMITER ;
~~~
##EX2
~~~mysql
DELIMITER //
DROP FUNCTION IF EXISTS spPotencia //
CREATE FUNCTION spPotencia(pBase INT, pExponent INT)
RETURNS INT DETERMINISTIC
BEGIN
	DECLARE vReturn INT;
	DECLARE vPotencia INT;
    
	IF pBase IS NOT NULL AND pExponent IS NOT NULL THEN
		SET vPotencia = pExponent;
		SET vReturn = pBase;

		WHILE (vPotencia > 0) DO
			SET vReturn = vReturn * pBase;
			SET vPotencia = vPotencia - 1;
		END WHILE;
    END IF;
    
	RETURN vReturn;
END
//
DELIMITER ;
~~~
##EX3
~~~mysql
DELIMITER //
DROP FUNCTION IF EXISTS spIncrement //
CREATE FUNCTION spIncrement(pCodiEmpleat INT, pIncrement INT)
RETURNS FLOAT NOT DETERMINISTIC READS SQL DATA
BEGIN
	DECLARE vReturn FLOAT;
    DECLARE vSalari FLOAT;
    
    IF pCodiEmpleat IS NOT NULL AND pIncrement IS NOT NULL THEN
		SELECT salari
			FROM empleats
		WHERE empleat_id = pCodiEmpleat INTO vSalari;
		SET vReturn = vSalari + (vSalari * pIncrement / 100);
    END IF;
    
    RETURN vReturn;
END
//
DELIMITER ;

~~~
##EX4
~~~mysql
DELIMITER //
DROP FUNCTION IF EXISTS spPringat //
CREATE FUNCTION spPringat(pCodiDep INT)
RETURNS INT NOT DETERMINISTIC READS SQL DATA
BEGIN
	DECLARE vReturn INT;
    DECLARE vSalari INT;
    SET vSalari = (SELECT MIN(salari)
						FROM empleats
					WHERE departament_id = pCodiDep);
	SET vReturn = (SELECT empleat_id
						FROM empleats
					WHERE departament_id = pCodiDep && salari = vSalari);
	RETURN vReturn;
END
//
DELIMITER ;
~~~
##EX5
~~~mysql

~~~
##EX6
~~~mysql

~~~
##EX7
~~~mysql

~~~
##EX8
~~~mysql

~~~
##EX9
~~~mysql

~~~
##EX10
~~~mysql

~~~

