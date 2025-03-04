# CheatSheet_SQL

## 1. Consultas Básicas y Joins

### Select Básico:
```sql
SELECT columna1, columna2
FROM tabla;
```

### Select con WHERE:
```sql
SELECT columna1, columna2
FROM tabla
WHERE condicion;
```

### Joins:
#### INNER JOIN (solo registros coincidentes):
```sql
SELECT t1.columna1, t2.columna2
FROM tabla1 t1
INNER JOIN tabla2 t2 ON t1.id = t2.id;

```
#### LEFT JOIN (incluye todos los registros de la tabla izquierda):
```sql
SELECT t1.columna1, t2.columna2
FROM tabla1 t1
LEFT JOIN tabla2 t2 ON t1.id = t2.id;
```
#### RIGHT JOIN (incluye todos los registros de la tabla derecha):
```sql
SELECT t1.columna1, t2.columna2
FROM tabla1 t1
RIGHT JOIN tabla2 t2 ON t1.id = t2.id;
```
#### FULL OUTER JOIN (todos los registros de ambas tablas):
```sql
SELECT t1.columna1, t2.columna2
FROM tabla1 t1
FULL OUTER JOIN tabla2 t2 ON t1.id = t2.id;
```
## 2. Subconsultas
### Subconsulta en el WHERE:
```sql
SELECT columna1
FROM tabla
WHERE columna2 = (SELECT MAX(columna2) FROM tabla);
```

### Subconsulta en el SELECT:
```sql
SELECT columna1, 
       (SELECT MAX(columna2) FROM tabla2) AS max_columna2
FROM tabla1;
```

## 3. Operadores adicionales

### IN (para verificar varios valores):

```sql
SELECT columna1 FROM tabla WHERE columna1 IN (valor1, valor2, valor3);
```
### BETWEEN (rango de valores):

```sql
SELECT columna1 FROM tabla WHERE columna2 BETWEEN valor1 AND valor2;
```
### LIKE (coincidencia de patrones):

```sql
SELECT columna1 FROM tabla WHERE columna2 LIKE 'A%';  -- Comienza con 'A'
SELECT columna1 FROM tabla WHERE columna2 LIKE '%ABC';  -- Termina con 'ABC'
SELECT columna1 FROM tabla WHERE columna2 LIKE '%123%';  -- Contiene '123'
```

## 4. Funciones de agregación
### COUNT:
```sql
SELECT COUNT(*) FROM tabla;
```
### SUM:
```sql
SELECT SUM(columna) FROM tabla;
```
### AVG:
```sql
SELECT AVG(columna) FROM tabla;
```
### MIN y MAX:
```sql
SELECT MIN(columna), MAX(columna) FROM tabla;
```
### GROUP BY:
```sql
SELECT columna, COUNT(*)
FROM tabla
GROUP BY columna;
```
### HAVING (filtra después de GROUP BY):
```sql
SELECT columna, COUNT(*)
FROM tabla
GROUP BY columna
HAVING COUNT(*) > 5;
```


## 5. Consultas de fechas y horas

### Fecha y hora actual:

```sql
SELECT CURRENT_DATE;  -- Fecha actual
SELECT CURRENT_TIME;  -- Hora actual
SELECT CURRENT_TIMESTAMP;  -- Fecha y hora actual
```
### Funciones de fecha:

```sql
SELECT DATE_ADD(fecha, INTERVAL 1 DAY) FROM tabla;  -- Sumar un día a la fecha
SELECT DATE_SUB(fecha, INTERVAL 1 MONTH) FROM tabla;  -- Restar un mes a la fecha
SELECT YEAR(fecha) FROM tabla;  -- Extraer el año de una fecha
SELECT MONTH(fecha) FROM tabla;  -- Extraer el mes de una fecha
SELECT DAY(fecha) FROM tabla;  -- Extraer el día de una fecha
```
### Formato de Fechas:

```sql
SELECT DATE_FORMAT(fecha, '%Y-%m-%d') FROM tabla;  -- Formato personalizado
```

## 6. Manipulación de cadenas de texto

### Concatenar cadenas:

```sql
SELECT CONCAT(cadena1, cadena2) FROM tabla;  -- Une dos cadenas
```
### Buscar y reemplazar subcadenas:

```sql
SELECT REPLACE(cadena, 'buscado', 'reemplazo') FROM tabla;  -- Reemplaza una subcadena
SELECT SUBSTRING(cadena, 1, 5) FROM tabla;  -- Extrae una subcadena
```
### Longitud de la cadena:

```sql
SELECT LENGTH(cadena) FROM tabla;  -- Longitud de la cadena
```



## 7. Funciones de ventana (Window Functions)
### ROW_NUMBER() (asigna un número único a cada fila dentro de una partición):
```sql
SELECT columna, 
       ROW_NUMBER() OVER (PARTITION BY columna ORDER BY columna2) AS row_num
FROM tabla;
```
### RANK() (asigna un rango, manejando empates):
```sql
SELECT columna, 
       RANK() OVER (ORDER BY columna2 DESC) AS rank
FROM tabla;
```
### DENSE_RANK() (asigna un rango sin dejar huecos por empates):
```sql
SELECT columna, 
       DENSE_RANK() OVER (ORDER BY columna2 DESC) AS dense_rank
FROM tabla;
```
### NTILE() (divide los resultados en una cantidad de particiones):
```sql
SELECT columna, 
       NTILE(4) OVER (ORDER BY columna2) AS quartile
FROM tabla;
```
## 8. Operaciones avanzadas
### Union (combina resultados de dos consultas):
```sql
SELECT columna1 FROM tabla1
UNION
SELECT columna1 FROM tabla2;
```
### Intersect (devuelve filas comunes entre dos consultas):
```sql
SELECT columna1 FROM tabla1
INTERSECT
SELECT columna1 FROM tabla2;
```
### Except (devuelve filas de la primera consulta que no están en la segunda):
```sql
SELECT columna1 FROM tabla1
EXCEPT
SELECT columna1 FROM tabla2;
```
## 9. Modificaciones de datos
### Insertar datos:
```sql
INSERT INTO tabla (columna1, columna2)
VALUES (valor1, valor2);
```
### Actualizar datos:
```sql
UPDATE tabla
SET columna1 = valor1
WHERE columna2 = valor2;
```
### Eliminar datos:
```sql
DELETE FROM tabla
WHERE condicion;
```

## 10. Índices
### Crear un índice:
```sql
CREATE INDEX index_name
ON tabla (columna);
```
### Eliminar un índice:
```sql
DROP INDEX index_name;
```


## 11. Transacciones
### Iniciar una transacción:
```sql
BEGIN TRANSACTION;
```
### Confirmar una transacción (commit):
```sql
COMMIT;
```
### Deshacer una transacción (rollback):
```sql
ROLLBACK;
```

## 12. Vistas (Views)

### Crear una Vista:

```sql
CREATE VIEW vista_nombre AS
SELECT columna1, columna2
FROM tabla
WHERE columna3 = 'valor';
```
### Eliminar una Vista:
```sql
DROP VIEW vista_nombre;
```


## 13. Seguridad y control de accesos
### Crear usuario:
```sql
CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'contraseña';
```
### Otorgar privilegios:
```sql
GRANT ALL PRIVILEGES ON base_de_datos.* TO 'usuario'@'localhost';
```
### Revocar privilegios:
```sql
REVOKE ALL PRIVILEGES ON base_de_datos.* FROM 'usuario'@'localhost';
```
### Eliminar usuario:
```sql
DROP USER 'usuario'@'localhost';
```


## 14. Optimización y plan de ejecución
### EXPLAIN (ver el plan de ejecución de una consulta):
```sql
EXPLAIN SELECT * FROM tabla WHERE columna = valor;
```
Uso de índices para mejorar la velocidad de las consultas.
Evitar SELECT * (seleccionar solo las columnas necesarias).
Considerar el uso de particiones para grandes conjuntos de datos.




## 15. Subconsultas avanzadas

### Subconsulta correlacionada (se refiere a columnas de la consulta externa):
```sql
SELECT columna1
FROM tabla1 t1
WHERE columna2 > (SELECT AVG(columna2) FROM tabla2 t2 WHERE t2.id = t1.id);
```
## 16. Consultas de texto completo

### Búsqueda de texto completo ( OJO: si la base de datos lo soporta):
```sql
SELECT columna1
FROM tabla
WHERE MATCH(columna1) AGAINST ('texto de búsqueda' IN NATURAL LANGUAGE MODE);
```

## 17. Funciones definidas por el usuario (UDFs)
 Función que el usuario puede definir en el sistema de gestión de bases de datos (DBMS).
 P.ej: Función multiplicar
### Crear una función:

```sql
CREATE FUNCTION funcion_nombre(parametro1 INT) RETURNS INT
BEGIN
  RETURN parametro1 * 2;
END;
```
### Llamar a una función:

```sql
SELECT funcion_nombre(5);  -- Llamada a la función
```
## 18. Procedimientos almacenados
Conjunto de instrucciones SQL predefinidas que se pueden almacenar y ejecutar en la base de datos.
### Crear un procedimiento almacenado:

```sql
CREATE PROCEDURE procedimiento_nombre()
BEGIN
  -- Lógica del procedimiento
  SELECT * FROM tabla;
END;
```
### Llamar a un procedimiento almacenado:
```sql
CALL procedimiento_nombre();
```
