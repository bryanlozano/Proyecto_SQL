![Universidad Nacional Hermilio Valdizán](./Picture/Unheval.png)
# Proyecto SQL: Análisis Académico de Egresados - Rendimiento y Trayectoria Universitaria

## Resumen (Overview)
*Este proyecto tiene como objetivo analizar la información académica y demográfica de **los egresados de pregrado de la Universidad Nacional Hermilio Valdizán (UNHEVAL) durante el año 2024**.*

_A partir de un dataset anonimizado de egresados, se desarrolló un proceso de análisis utilizando SQL y un modelo dimensional tipo estrella para explorar indicadores relacionados con el perfil de los estudiantes, su rendimiento académico, procedencia geográfica, modalidad de estudios y trayectoria universitaria._

_El análisis busca transformar datos académicos en información útil para la toma de decisiones, permitiendo identificar patrones en el desempeño de los egresados, comparar resultados entre escuelas académicas y modalidades de estudio, así como analizar el tiempo transcurrido desde la primera matrícula hasta el egreso._

_Como parte del proyecto, se diseñaron consultas SQL de complejidad progresiva que incorporan técnicas como **agregaciones, JOINs, CASE WHEN, CTEs y Window Functions** para responder preguntas de negocio relevantes dentro del contexto de la educación superior._

_El resultado es un análisis estructurado que permite generar insights sobre rendimiento académico, eficiencia en la trayectoria formativa y características de la población de egresados._

## Objetivo de negocio
Analizar la información académica y demográfica de los egresados de pregrado de la Universidad Nacional Hermilio Valdizán durante el año 2024, con el propósito de identificar patrones de rendimiento académico, trayectoria universitaria, procedencia geográfica y eficiencia en el tiempo de formación que contribuyan a la toma de decisiones institucionales.

## Objetivos específicos
1. Analizar la distribución de egresados según escuela académica, sexo, modalidad de estudio y sede.
2. Identificar el perfil demográfico y geográfico de los egresados.
3. Evaluar el rendimiento académico mediante el análisis del promedio final por diferentes dimensiones.
4. Comparar el desempeño académico entre escuelas académicas y modalidades de estudio.
5. Analizar las cohortes de ingreso según el año y semestre de primera matrícula.
6. Calcular el tiempo de formación académica desde la primera matrícula hasta el egreso.
7. Identificar escuelas con mayor eficiencia académica considerando el tiempo promedio requerido para egresar.
8. Segmentar a los egresados según su rendimiento académico para identificar patrones de alto y bajo desempeño.
9. Construir rankings académicos y geográficos mediante técnicas avanzadas de SQL.

## Estructura del Proyecto

- [Sobre los Datos](#sobre-los-datos)
- [Tareas](#tareas)
- [Limpieza de Datos](#limpieza-de-datos)
- [Análisis Exploratorio de Datos e Insights](#análisis-exploratorio-de-datos-e-insights)

## Sobre los Datos

Los datos originales, junto con una explicación de cada columna, se pueden encontrar [aquí](https://www.datosabiertos.gob.pe/dataset/alumnos-egresados-de-pregrado-de-la-universidad-nacional-hermilio-valdiz%C3%A1n-2024-unheval).

El dataset fue transformado y normalizado en un modelo relacional compuesto por tres tablas principales:

`Dim_Escuela`
`Dim_Ubicacion`
`Fact_Egresados`

La normalización permitió garantizar:

- ✅ Integridad de los datos
- ✅ Reducción de redundancia
- ✅ Mayor eficiencia en consultas SQL
- ✅ Mejor organización de la información
- ✅ Escalabilidad para futuros dashboards y modelos predictivos


![Universidad Nacional Hermilio Valdizán](./Picture/Unheval.png)

## Tareas (Task)

En este análisis, ayudo al área de Gestión Académica a calcular lo siguiente:

1. **Distribución de egresados por escuela académica**
🎯 Negocio: La universidad quiere conocer qué escuelas concentran más egresados.
📊 Reto: Contar egresados por escuela.
🧠 SQL: GROUP BY, COUNT(*)
2. Distribución de egresados por sexo

🎯 Negocio: Analizar equidad de género en egresados.
📊 Reto: Número y porcentaje por sexo.
🧠 SQL: GROUP BY, COUNT, cálculo de porcentaje.
4. Edad promedio de los egresados

🎯 Negocio: Identificar perfil etario del egresado.
📊 Reto: Promedio, mínimo y máximo de edad.
🧠 SQL: AVG(), MIN(), MAX()

5. Número de egresados por departamento de nacimiento

🎯 Negocio: Identificar zonas geográficas de mayor procedencia.
📊 Reto: Agrupar por Dim_Ubicacion.Departamento
🧠 SQL: JOIN + GROUP BY

----------------
6. Top 5 escuelas con mayor promedio académico

🎯 Negocio: Detectar escuelas con mejor desempeño académico.
📊 Reto: Ranking de escuelas por promedio final.
🧠 SQL: GROUP BY + ORDER BY + TOP/LIMIT

8. Tiempo promedio de formación (matrícula vs egreso)

🎯 Negocio: Medir eficiencia académica.
📊 Reto: Diferencia entre ANIO_EGRESO y ANIO_MATRICULA1.
🧠 SQL: DATEDIFF logic + agregación
9. Egresados por cohorte de ingreso (año de matrícula)

🎯 Negocio: Analizar generaciones de ingreso.
📊 Reto: Agrupar por ANIO_MATRICULA1.
🧠 SQL: GROUP BY
10. Distribución de edad por escuela académica

🎯 Negocio: Identificar perfiles etarios por carrera.
📊 Reto: Edad promedio por escuela.
🧠 SQL: GROUP BY Dim_Escuela

----------------

11. Ranking de escuelas por eficiencia académica (tiempo de egreso)

🎯 Negocio: Identificar escuelas donde los alumnos egresan más rápido.
📊 Reto: Promedio de duración por escuela + ranking.
🧠 SQL:

DATEDIFF(anio_egreso, anio_matricula1)
WINDOW FUNCTION (RANK())

13. Segmentación de egresados por rendimiento (CASE WHEN)

🎯 Negocio: Clasificar estudiantes según desempeño académico.
📊 Reto: Crear categorías:

Bajo (<13)
Medio (13–15)
Alto (>15)
🧠 SQL: CASE WHEN

14. Top provincias con mejores promedios académicos

🎯 Negocio: Analizar calidad académica según origen geográfico.
📊 Reto: Promedio final por provincia + ranking.
🧠 SQL: JOIN Dim_Ubicacion + WINDOW FUNCTION

15. Análisis combinado: perfil del egresado ideal

🎯 Negocio: Identificar combinación óptima de atributos de alto rendimiento.
📊 Reto: Cruce de:

Escuela
Modalidad
Sexo
Ubicación
con filtro de PROMEDIO_FINAL alto (ej. > 15)
🧠 SQL:
CTEs múltiples
CASE WHEN
GROUP BY múltiples dimensiones
WINDOW FUNCTIONS


## Limpieza de Datos

Antes de realizar el análisis, es fundamental asegurar que los datos estén limpios y listos. Dado que las tablas `EducationLevel`, `RatingLevel` y `SatisfiedLevel` son de referencia, el trabajo principal se centra en las tablas `Employee` y `PerformanceRating`.

#### Valores Nulos o Faltantes

Primero, verifiqué la existencia de valores faltantes en los dos campos clave: `EmployeeID` y `PerformanceID`. No se encontraron valores nulos.

```sql
-- Verificar valores faltantes en la tabla Employee --

SELECT COUNT(*) AS MissingValues
FROM Employee
WHERE EmployeeID IS NULL;

--Verificar valores faltantes en la tabla PerformanceRating--

SELECT COUNT(*) AS MissingValues
FROM PerformanceRating
WHERE PerformanceID IS NULL
    OR EmployeeID IS NULL;
```

A continuación, es vital asegurarse de que se eliminen las filas duplicadas, en caso de encontrarse, nuevamente en los campos clave. No se encontraron duplicados.

```sql
-- Verificar valores duplicados en la tabla Employe --

SELECT EmployeeID, COUNT(*)
FROM Employee
GROUP BY EmployeeID
HAVING COUNT(*) > 1;

-- Verificar valores duplicados en la tabla PerformanceRating --

SELECT PerformanceID, COUNT(*)
FROM PerformanceRating
GROUP BY PerformanceID
HAVING COUNT(*) > 1;
```


## Análisis Exploratorio de Datos (EDA) e Insights

### Pregunta #1: Distribución de egresados por escuela académica

Encontré.

```sql
-- Egresados por escuela académica --
SELECT
    e.ESCUELA_ACADEMICA,
    COUNT(*) AS total_egresados
FROM Fact_Egresados f
JOIN Dim_Escuela e ON f.COD_ESCUELA = e.COD_ESCUELA
GROUP BY e.ESCUELA_ACADEMICA
ORDER BY total_egresados DESC;
```

![image](./picture/P1.png)

### Pregunta #2: Distribución de egresados por sexo

Para .

```sql
-- Egresados por sexo (cantidad y porcentaje) --
SELECT 
    SEXO,
    COUNT(*) AS total,
    ROUND(100.0 * COUNT(*) / SUM(COUNT(*)) OVER(), 2) AS porcentaje
FROM Fact_Egresados
GROUP BY SEXO
```

![image](./picture/P2.png)


### Pregunta #4: Edad promedio de los egresados

A continuación.

```sql
-- Edad promedio de egresados --
SELECT 
    AVG(EDAD) AS edad_promedio,
    MIN(EDAD) AS edad_min,
    MAX(EDAD) AS edad_max
FROM Fact_Egresados;

```

![image](./picture/P3.png)


### Pregunta #5: Número de egresados por departamento de nacimiento

Para este problema

```sql
-- Egresados por departamento --
SELECT 
    u.DEPARTAMENTO,
    COUNT(*) AS total_egresados
FROM Fact_Egresados f
JOIN Dim_Ubicacion u ON f.UBIGEO = u.UBIGEO
GROUP BY u.DEPARTAMENTO
ORDER BY total_egresados DESC;
```

### Pregunta #6: Top 5 escuelas con mayor promedio académico

Aquí.

```sql
-- Top 5 escuelas por promedio final
SELECT TOP 5
    e.ESCUELA_ACADEMICA,
    AVG(f.PROMEDIO_FINAL) AS promedio
FROM Fact_Egresados f
JOIN Dim_Escuela e ON f.COD_ESCUELA = e.COD_ESCUELA
GROUP BY e.ESCUELA_ACADEMICA
ORDER BY promedio DESC
```

![image](./picture/P6.png)


### Pregunta #8: Tiempo promedio de formación (matrícula vs egreso)

Primero.

```sql
-- Tiempo promedio de formación --

select avg(
case 
when SEMESTRE_EGRESO = SEMESTRE_MATRICULA1 then (ANIO_EGRESO-ANIO_MATRICULA1)+0.5
when SEMESTRE_EGRESO > SEMESTRE_MATRICULA1 then (ANIO_EGRESO-ANIO_MATRICULA1)+1
when SEMESTRE_EGRESO < SEMESTRE_MATRICULA1 then (ANIO_EGRESO-ANIO_MATRICULA1)
else 'ERROR'
end) as prom_anios_estudio
FROM Fact_Egresados
```


### Pregunta #9: Egresados por cohorte de ingreso (año de matrícula)

Para.

```sql
-- Egresados por peiodo de ingreso (Fecha de corte 30/06/2025) / DEBERÍA VERSE POR AÑO DE EGRESO EN COLUMNA
SELECT 
    ANIO_MATRICULA1,
    COUNT(*) AS total_egresados
FROM Fact_Egresados
GROUP BY ANIO_MATRICULA1
ORDER BY ANIO_MATRICULA1;
```

### Pregunta #10: Distribución de edad por escuela académica
```sql
-- Edad promedio por escuela --
SELECT 
    e.ESCUELA_ACADEMICA,
    AVG(f.EDAD) AS edad_promedio
FROM Fact_Egresados f
JOIN Dim_Escuela e ON f.COD_ESCUELA = e.COD_ESCUELA
GROUP BY e.ESCUELA_ACADEMICA
ORDER BY edad_promedio DESC;
```

### Pregunta #11: Ranking de escuelas por eficiencia académica (tiempo de egreso)
```sql
-- Ranking de escuelas por tiempo de egreso / VERIFICAR EXACTITUD --
SELECT 
    e.ESCUELA_ACADEMICA,
    AVG(f.ANIO_EGRESO - f.ANIO_MATRICULA1) AS tiempo_promedio,
    RANK() OVER (
        ORDER BY AVG(f.ANIO_EGRESO - f.ANIO_MATRICULA1)
    ) AS ranking
FROM Fact_Egresados f
JOIN Dim_Escuela e ON f.COD_ESCUELA = e.COD_ESCUELA
GROUP BY e.ESCUELA_ACADEMICA;
-----------------------
SELECT
    e.ESCUELA_ACADEMICA,
    COUNT(*) AS TOTAL_EGRESADOS,
    ROUND(
        AVG(
            (f.ANIO_EGRESO * 2 + f.SEMESTRE_EGRESO)
            - (f.ANIO_MATRICULA1 * 2 + f.SEMESTRE_MATRICULA1)
        ),
        2
    ) AS PROMEDIO_SEMESTRES,
    ROUND(
        AVG(
            (
                (f.ANIO_EGRESO * 2 + f.SEMESTRE_EGRESO)
                - (f.ANIO_MATRICULA1 * 2 + f.SEMESTRE_MATRICULA1)
            ) / 2.0
        ),
        2
    ) AS PROMEDIO_ANIOS,
    RANK() OVER (
        ORDER BY AVG(
            (f.ANIO_EGRESO * 2 + f.SEMESTRE_EGRESO)
            - (f.ANIO_MATRICULA1 * 2 + f.SEMESTRE_MATRICULA1)
        ) ASC
    ) AS RANKING_EFICIENCIA
FROM Fact_Egresados f
INNER JOIN Dim_Escuela e
    ON f.COD_ESCUELA = e.COD_ESCUELA
GROUP BY
    e.ESCUELA_ACADEMICA
ORDER BY
    RANKING_EFICIENCIA,
    TOTAL_EGRESADOS DESC;
```

### Pregunta #13: Segmentación de egresados por rendimiento (CASE WHEN)
```sql
-- Segmentación por rendimiento (CASE WHEN) --
SELECT 
    UUID,
    PROMEDIO_FINAL,
    CASE 
        WHEN PROMEDIO_FINAL < 13 THEN 'Bajo'
        WHEN PROMEDIO_FINAL BETWEEN 13 AND 15 THEN 'Medio'
        ELSE 'Alto'
    END AS categoria_rendimiento
FROM Fact_Egresados;
```

### Pregunta #14: Top provincias con mejores promedios académicos
```sql
-- Top provincias por rendimiento --
SELECT TOP 10
    u.PROVINCIA,
    AVG(f.PROMEDIO_FINAL) AS promedio
FROM Fact_Egresados f
JOIN Dim_Ubicacion u ON f.UBIGEO = u.UBIGEO
GROUP BY u.PROVINCIA
ORDER BY promedio DESC
```

### Pregunta #15: Análisis combinado: perfil del egresado ideal
```sql
-- Perfil del egresado de alto rendimiento --
SELECT 
    e.ESCUELA_ACADEMICA,
    SEXO,
    u.DEPARTAMENTO,
    AVG(f.PROMEDIO_FINAL) AS promedio_alto_rendimiento,
    COUNT(*) AS total_egresados
FROM Fact_Egresados f
JOIN Dim_Escuela e ON f.COD_ESCUELA = e.COD_ESCUELA
JOIN Dim_Ubicacion u ON f.UBIGEO = u.UBIGEO
WHERE f.PROMEDIO_FINAL > 15
GROUP BY 
    e.ESCUELA_ACADEMICA,
    SEXO,
    u.DEPARTAMENTO
ORDER BY promedio_alto_rendimiento DESC;
```

### Conclusion

- Este.