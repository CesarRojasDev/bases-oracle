# Oracle SQL - Guía Rápida

## Índice

### SQL

- [Consultas Básicas](#consultas-básicas)
  - [Seleccionar datos](#seleccionar-datos)
  - [Alias](#alias)
  - [DISTINCT](#distinct)
- [Filtros](#filtros)
  - [WHERE](#where)
  - [IN](#in)
  - [BETWEEN](#between)
  - [LIKE](#like)
  - [NULL](#null)
- [Ordenamiento](#ordenamiento)
  - [Ascendente](#ascendente)
  - [Descendente](#descendente)
  - [Múltiples columnas](#múltiples-columnas)
- [Top N registros](#top-n-registros)
  - [Oracle 12c+](#oracle-12c)
  - [Registro más reciente](#registro-más-reciente)
- [Fechas](#fechas)
- [Funciones de Texto](#funciones-de-texto)
  - [UPPER](#upper)
  - [LOWER](#lower)
  - [INITCAP](#initcap)
  - [LENGTH](#length)
  - [SUBSTR](#substr)
  - [REPLACE](#replace)
  - [TRIM](#trim)
  - [INSTR](#instr)
  - [CONCAT](#concat)
- [Funciones de Fechas](#funciones-de-fechas)
  - [SYSDATE](#sysdate)
  - [SYSTIMESTAMP](#systimestamp)
  - [TRUNC](#trunc)
  - [ADD_MONTHS](#add_months)
  - [MONTHS_BETWEEN](#months_between)
  - [TO_CHAR](#to_char)
  - [TO_DATE](#to_date)
- [Funciones Nulas](#funciones-nulas)
  - [NVL](#nvl)
  - [COALESCE](#coalesce)
- [Funciones Numéricas](#funciones-numéricas)
  - [ROUND](#round)
  - [TRUNC (numérico)](#trunc-numérico)
  - [CEIL](#ceil)
  - [FLOOR](#floor)
- [CASE](#case)
- [Funciones de Agregación](#funciones-de-agregación)
  - [COUNT](#count)
  - [SUM](#sum)
  - [AVG](#avg)
  - [MIN](#min)
  - [MAX](#max)
- [JOINs](#joins)
  - [INNER JOIN](#inner-join)
  - [LEFT JOIN](#left-join)
- [WITH (CTE)](#with-cte)
- [CASE (por valor de columna)](#case-por-valor-de-columna)
- [EXISTS](#exists)
- [UPDATE](#update)
- [DELETE](#delete)
- [INSERT](#insert)
- [MERGE (UPSERT)](#merge-upsert)
- [Transacciones](#transacciones)
- [DUAL](#dual)
- [Diccionario de Datos](#diccionario-de-datos)
- [JSON](#json)
  - [JSON_OBJECT](#json_object)
  - [JSON_ARRAY](#json_array)
  - [JSON_VALUE](#json_value)
  - [JSON_QUERY](#json_query)
  - [JSON_TABLE](#json_table)

### PL/SQL

- [Bloque Anónimo](#bloque-anónimo)
- [Variables](#variables)
- [IF](#if)
- [IF ELSE](#if-else)
- [LOOP](#loop)
- [FOR](#for)
- [WHILE](#while)
- [SELECT INTO](#select-into)
- [Manejo de Excepciones](#manejo-de-excepciones)
- [Procedimiento](#procedimiento)
- [Parámetros IN](#parámetros-in)
- [Parámetros OUT](#parámetros-out)
- [Cursor FOR](#cursor-for)
- [Buenas Prácticas](#buenas-prácticas)

---

## Consultas Básicas

### Seleccionar datos

```sql
SELECT *
FROM PS_COMPRA;
```

### Alias

```sql
SELECT
    C.SKU,
    C.IMEI
FROM PS_COMPRA C;
```

### DISTINCT

```sql
SELECT DISTINCT ESTADO
FROM PS_COMPRA;
```

---

## Filtros

### WHERE

```sql
SELECT *
FROM PS_PRODUCTO
WHERE NOMBRE_PRODUCTO = 'iPhone 16 C/CHIP 128GB 8GB Azul';
```

### IN

```sql
SELECT *
FROM PS_COMPRA
WHERE ESTADO IN ('REGISTRAR', 'CERRADO');
```

### BETWEEN

```sql
SELECT *
FROM PS_COMPRA
WHERE FECHA BETWEEN DATE '2026-01-01' AND DATE '2026-01-31';
```

### LIKE

```sql
SELECT *
FROM PS_PRODUCTO
WHERE SKU LIKE 'CELU%';
```

### NULL

```sql
SELECT *
FROM PS_PRODUCTO
WHERE SKU IS NULL;
```

---

## Ordenamiento

### Ascendente

```sql
ORDER BY FECHA;
```

### Descendente

```sql
ORDER BY FECHA DESC;
```

### Múltiples columnas

```sql
ORDER BY FECHA DESC, CODIGO DESC;
```

---

## Top N registros

### Oracle 12c+

```sql
SELECT *
FROM PS_COMPRA
FETCH FIRST 10 ROWS ONLY;
```

### Registro más reciente

```sql
SELECT *
FROM PS_COMPRA
ORDER BY FECHA DESC
FETCH FIRST 1 ROW ONLY;
```

---

## Fechas

### Fecha actual

```sql
SYSDATE
```

### Fecha y hora actual

```sql
SYSTIMESTAMP
```

### Truncar hora

```sql
TRUNC(SYSDATE)
```

### Sumar días

```sql
SYSDATE + 7
```

### Restar días

```sql
SYSDATE - 30
```

### Formato fecha

```sql
TO_CHAR(SYSDATE, 'DD/MM/YYYY')
```

```sql
TO_CHAR(SYSDATE, 'DD/MM/YYYY HH24:MI:SS')
```

### Convertir texto a fecha

```sql
TO_DATE('23/06/2026', 'DD/MM/YYYY')
```

---
## Funciones de Texto

### UPPER

Convierte todo a mayúsculas.

```sql
SELECT UPPER('Cesar Rojas')
FROM DUAL;
```

Resultado:

```text
CESAR ROJAS
```

---

### LOWER

Convierte todo a minúsculas.

```sql
SELECT LOWER('Cesar Rojas')
FROM DUAL;
```

Resultado:

```text
cesar rojas
```

---

### INITCAP

Primera letra de cada palabra en mayúscula.

```sql
SELECT INITCAP('cesar rojas turkowsky')
FROM DUAL;
```

Resultado:

```text
Cesar Rojas Turkowsky
```

---

### LENGTH

Obtiene la cantidad de caracteres.

```sql
SELECT LENGTH('ORACLE')
FROM DUAL;
```

Resultado:

```text
6
```

---

### SUBSTR

Extrae una parte del texto.

```sql
SELECT SUBSTR('ANGULAR',1,3)
FROM DUAL;
```

Resultado:

```text
ANG
```

```sql
SELECT SUBSTR('ANGULAR',4)
FROM DUAL;
```

Resultado:

```text
ULAR
```

---

### REPLACE

Reemplaza texto.

```sql
SELECT REPLACE('CESAR','A','X')
FROM DUAL;
```

Resultado:

```text
CESXR
```

---

### TRIM

Elimina espacios al inicio y final.

```sql
SELECT TRIM('   CESAR   ')
FROM DUAL;
```

Resultado:

```text
CESAR
```

---

### INSTR

Busca la posición de un texto.

```sql
SELECT INSTR('ANGULAR','GU')
FROM DUAL;
```

Resultado:

```text
3
```

---

### CONCAT

Concatena cadenas.

```sql
SELECT CONCAT('CESAR',' ROJAS')
FROM DUAL;
```

Resultado:

```text
CESAR ROJAS
```

También:

```sql
SELECT 'CESAR' || ' ROJAS'
FROM DUAL;
```

Resultado:

```text
CESAR ROJAS
```

---

## Funciones de Fechas

### SYSDATE

Fecha actual.

```sql
SELECT SYSDATE
FROM DUAL;
```

Resultado:

```text
23/06/2026 17:24:43
```

---

### SYSTIMESTAMP

Fecha con precisión de milisegundos.

```sql
SELECT SYSTIMESTAMP
FROM DUAL;
```

Resultado:

```text
23/06/26 17:24:54,119000 -05:00
```

---

### TRUNC

Quita la hora.

```sql
SELECT TRUNC(SYSDATE)
FROM DUAL;
```

Resultado:

```text
23/06/2026
```

---

### ADD_MONTHS

Agregar meses.

```sql
SELECT ADD_MONTHS(SYSDATE,1)
FROM DUAL;
```

Resultado:

```text
23/07/2026
```

---

### MONTHS_BETWEEN

Diferencia entre fechas en meses.

```sql
SELECT MONTHS_BETWEEN(
       DATE '2026-12-31',
       DATE '2026-06-30')
FROM DUAL;
```

Resultado:

```text
6
```

---

### TO_CHAR

Convertir fecha a texto.

```sql
SELECT TO_CHAR(SYSDATE,'DD/MM/YYYY')
FROM DUAL;
```

Resultado:

```text
23/06/2026
```

```sql
SELECT TO_CHAR(SYSDATE,'DD/MM/YYYY HH24:MI:SS')
FROM DUAL;
```

Resultado:

```text
23/06/2026 18:45:32
```

---

### TO_DATE

Convertir texto a fecha.

```sql
SELECT TO_DATE(
       '23/06/2026',
       'DD/MM/YYYY')
FROM DUAL;
```

Resultado:

```text
23/06/2026
```

---

## Funciones Nulas

### NVL

Si es NULL devuelve otro valor.

```sql
SELECT NVL(NULL,0)
FROM DUAL;
```

Resultado:

```text
0
```

```sql
SELECT NVL(NULL,'SIN SKU')
FROM DUAL;
```

Resultado:

```text
SIN SKU
```

---

### COALESCE

Devuelve el primer valor no nulo.

```sql
SELECT COALESCE(
       NULL,
       NULL,
       'VALOR')
FROM DUAL;
```

Resultado:

```text
VALOR
```

---

## Funciones Numéricas

### ROUND

Redondear.

```sql
SELECT ROUND(15.678,2)
FROM DUAL;
```

Resultado:

```text
15.68
```

---

### TRUNC (numérico)

Eliminar decimales.

```sql
SELECT TRUNC(15.678,2)
FROM DUAL;
```

Resultado:

```text
15.67
```

---

### CEIL

Redondear hacia arriba.

```sql
SELECT CEIL(15.1)
FROM DUAL;
```

Resultado:

```text
16
```

---

### FLOOR

Redondear hacia abajo.

```sql
SELECT FLOOR(15.9)
FROM DUAL;
```

Resultado:

```text
15
```

---

## CASE

```sql
SELECT
    CASE
        WHEN 95 >= 70 THEN 'APROBADO'
        ELSE 'DESAPROBADO'
    END RESULTADO
FROM DUAL;
```

Resultado:

```text
APROBADO
```

---

## Funciones de Agregación

### COUNT

```sql
SELECT COUNT(*)
FROM PS_COMPRA;
```

Resultado:

```text
1250
```

---

### SUM

```sql
SELECT SUM(TOTAL)
FROM TB_VENTA;
```

Resultado:

```text
25487.50
```

---

### AVG

```sql
SELECT AVG(TOTAL)
FROM TB_VENTA;
```

Resultado:

```text
850.23
```

---

### MIN

```sql
SELECT MIN(FECHA)
FROM TB_VENTA;
```

Resultado:

```text
01/01/2026
```

---

### MAX

```sql
SELECT MAX(FECHA)
FROM TB_VENTA;
```

Resultado:

```text
23/06/2026
```

---

## JOINs

### INNER JOIN

```sql
SELECT *
FROM TB_VENTA V
INNER JOIN TB_VENTA_DETALLE D
    ON D.COD_VENTA = V.CODIGO;
```

### LEFT JOIN

```sql
SELECT *
FROM TB_VENTA V
LEFT JOIN TB_VENTA_DETALLE D
    ON D.COD_VENTA = V.CODIGO;
```

---

## WITH (CTE)

Permite crear consultas temporales para hacer el código más legible.

### Ejemplo

```sql
WITH COMPRAS_HOY AS
(
    SELECT *
    FROM PS_COMPRA
    WHERE TRUNC(FECHA) = TRUNC(SYSDATE)
)
SELECT *
FROM COMPRAS_HOY;
```

---

## CASE (por valor de columna)

```sql
SELECT
    CASE ESTADO
        WHEN 'A' THEN 'ACTIVO'
        WHEN 'I' THEN 'INACTIVO'
        ELSE 'DESCONOCIDO'
    END AS ESTADO_DESC
FROM PS_SEG_USUARIO;
```

---

## EXISTS

```sql
SELECT *
FROM PS_COMPRA C
WHERE EXISTS (
    SELECT 1
    FROM PS_COMPRA_OSIPTEL O
    WHERE O.IMEI_01 = C.IMEI
);
```

---

## UPDATE

```sql
UPDATE PS_COMPRA
SET ESTADO = 'CERRADO'
WHERE CODIGO = 1;
```

---

## DELETE

```sql
DELETE FROM PS_COMPRA
WHERE CODIGO = 1;
```

---

## INSERT

```sql
INSERT INTO PS_COMPRA
(
    CODIGO,
    SKU
)
VALUES
(
    1,
    'SKU001'
);
```

---

## MERGE (UPSERT)

```sql
MERGE INTO DESTINO D
USING ORIGEN O
ON (D.CODIGO = O.CODIGO)

WHEN MATCHED THEN
    UPDATE SET D.NOMBRE = O.NOMBRE

WHEN NOT MATCHED THEN
    INSERT (CODIGO, NOMBRE)
    VALUES (O.CODIGO, O.NOMBRE);
```

---

## Transacciones

### Confirmar

```sql
COMMIT;
```

### Revertir

```sql
ROLLBACK;
```

---

## DUAL

```sql
SELECT SYSDATE
FROM DUAL;
```

---

## Diccionario de Datos

### Ver columnas

```sql
SELECT *
FROM USER_TAB_COLUMNS
WHERE TABLE_NAME = 'PS_COMPRA';
```

### Ver índices

```sql
SELECT *
FROM USER_INDEXES
WHERE TABLE_NAME = 'PS_COMPRA';
```

### Ver triggers

```sql
SELECT *
FROM USER_TRIGGERS;
```

### Ver procedimientos

```sql
SELECT *
FROM USER_OBJECTS
WHERE OBJECT_TYPE = 'PROCEDURE';
```

---

## JSON

### JSON_OBJECT

Convierte columnas en un objeto JSON.

```sql
SELECT JSON_OBJECT(
           'codigo' VALUE CODIGO,
           'sku' VALUE SKU
       )
FROM PS_COMPRA;
```

Resultado:

```json
{
  "codigo": 1,
  "sku": "SKU001"
}
```

---

### JSON_ARRAY

Crea un arreglo JSON.

```sql
SELECT JSON_ARRAY(
           'APPLE',
           'SAMSUNG',
           'XIAOMI'
       )
FROM DUAL;
```

Resultado:

```json
["APPLE","SAMSUNG","XIAOMI"]
```

---

### JSON_VALUE

Obtiene un valor de un JSON.

```sql
SELECT JSON_VALUE(
           '{"marca":"Apple","modelo":"iPhone 16"}',
           '$.marca'
       )
FROM DUAL;
```

Resultado:

```text
Apple
```

---

### JSON_QUERY

Obtiene un objeto o arreglo JSON.

```sql
SELECT JSON_QUERY(
           '{"telefonos":["111","222"]}',
           '$.telefonos'
       )
FROM DUAL;
```

Resultado:

```json
["111","222"]
```

---

### JSON_TABLE

Convierte un JSON en filas.

```sql
SELECT *
FROM JSON_TABLE(
    '[
       {"sku":"SKU001","precio":100},
       {"sku":"SKU002","precio":200}
     ]',
    '$[*]'
    COLUMNS
    (
        SKU VARCHAR2(50) PATH '$.sku',
        PRECIO NUMBER PATH '$.precio'
    )
);
```

---

---

# PL/SQL

## Bloque Anónimo

```sql
BEGIN
    DBMS_OUTPUT.PUT_LINE('Hola Mundo');
END;
```

---

## Variables

```sql
DECLARE
    V_NOMBRE VARCHAR2(100);
BEGIN
    V_NOMBRE := 'Cesar';

    DBMS_OUTPUT.PUT_LINE(V_NOMBRE);
END;
```

---

## IF

```sql
DECLARE
    V_EDAD NUMBER := 18;
BEGIN
    IF V_EDAD >= 18 THEN
        DBMS_OUTPUT.PUT_LINE('Mayor de edad');
    END IF;
END;
```

---

## IF ELSE

```sql
DECLARE
    V_ESTADO VARCHAR2(1) := 'A';
BEGIN
    IF V_ESTADO = 'A' THEN
        DBMS_OUTPUT.PUT_LINE('Activo');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Inactivo');
    END IF;
END;
```

---

## LOOP

```sql
DECLARE
    V_CONTADOR NUMBER := 1;
BEGIN
    LOOP
        DBMS_OUTPUT.PUT_LINE(V_CONTADOR);

        V_CONTADOR := V_CONTADOR + 1;

        EXIT WHEN V_CONTADOR > 5;
    END LOOP;
END;
```

---

## FOR

```sql
BEGIN
    FOR I IN 1..5 LOOP
        DBMS_OUTPUT.PUT_LINE(I);
    END LOOP;
END;
```

---

## WHILE

```sql
DECLARE
    V_CONTADOR NUMBER := 1;
BEGIN
    WHILE V_CONTADOR <= 5 LOOP

        DBMS_OUTPUT.PUT_LINE(V_CONTADOR);

        V_CONTADOR := V_CONTADOR + 1;

    END LOOP;
END;
```

---

## SELECT INTO

```sql
DECLARE
    V_SKU VARCHAR2(100);
BEGIN
    SELECT SKU
    INTO V_SKU
    FROM PS_COMPRA
    WHERE CODIGO = 1;

    DBMS_OUTPUT.PUT_LINE(V_SKU);
END;
```

---

## Manejo de Excepciones

```sql
DECLARE
    V_SKU VARCHAR2(100);
BEGIN

    SELECT SKU
    INTO V_SKU
    FROM PS_COMPRA
    WHERE CODIGO = 999;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No existe registro');
END;
```

---

## Procedimiento

```sql
CREATE OR REPLACE PROCEDURE SP_SALUDAR
AS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Hola Mundo');
END;
```

Ejecutar:

```sql
BEGIN
    SP_SALUDAR;
END;
```

---

## Parámetros IN

```sql
CREATE OR REPLACE PROCEDURE SP_SALUDAR
(
    P_NOMBRE IN VARCHAR2
)
AS
BEGIN
    DBMS_OUTPUT.PUT_LINE(
        'Hola ' || P_NOMBRE
    );
END;
```

---

## Parámetros OUT

```sql
CREATE OR REPLACE PROCEDURE SP_OBTENER_TEXTO
(
    P_TEXTO OUT VARCHAR2
)
AS
BEGIN
    P_TEXTO := 'Hola Mundo';
END;
```

---

## Cursor FOR

```sql
BEGIN
    FOR R IN
    (
        SELECT SKU
        FROM PS_COMPRA
    )
    LOOP
        DBMS_OUTPUT.PUT_LINE(R.SKU);
    END LOOP;
END;
```

---

## Buenas Prácticas

* Siempre usar alias (`C`, `V`, `D`).
* Evitar `SELECT *` en producción.
* Filtrar antes de hacer JOIN.
* Usar índices en columnas de búsqueda frecuente.
* Manejar `NULL` con `NVL` o `COALESCE`.
* Revisar planes de ejecución para consultas lentas.
* Confirmar con `COMMIT` solo cuando todo haya terminado correctamente.
