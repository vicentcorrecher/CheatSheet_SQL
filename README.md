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
## 3. Funciones de Agregación
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

## 4. Funciones de Ventana (Window Functions)
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
## 5. Operaciones Avanzadas
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
## 6. Modificaciones de Datos
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
## 7. Transacciones
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
## 8. Índices
### Crear un índice:
```sql
CREATE INDEX index_name
ON tabla (columna);
```
### Eliminar un índice:
```sql
DROP INDEX index_name;
```
## 9. Optimización y Plan de Ejecución
### EXPLAIN (ver el plan de ejecución de una consulta):
```sql
EXPLAIN SELECT * FROM tabla WHERE columna = valor;
```
Uso de índices para mejorar la velocidad de las consultas.
Evitar SELECT * (seleccionar solo las columnas necesarias).
Considerar el uso de particiones para grandes conjuntos de datos.

## 10. Seguridad y Control de Accesos
### Crear usuario:
```sql
CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'contraseña';
```
### Otorgar privilegios:
```sql
GRANT ALL PRIVILEGES ON base_de_datos.* TO 'usuario'@'localhost';
```
Revocar privilegios:
```sql
REVOKE ALL PRIVILEGES ON base_de_datos.* FROM 'usuario'@'localhost';
```
### Eliminar usuario:
```sql
DROP USER 'usuario'@'localhost';
```
