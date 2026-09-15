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

🟢 Nivel básico
01. **Distribución de egresados por escuela:** ¿Cuántos egresados tiene cada escuela académica?

02. **Distribución de egresados por sexo:**
¿Cuál es la distribución de egresados según sexo y qué porcentaje representa cada grupo?

03. **Egresados por modalidad:**
¿Cuántos egresados corresponden a cada modalidad de estudio?

04. **Perfil etario:**
¿Cuál es la edad promedio, mínima y máxima de los egresados?

05. **Procedencia geográfica:**
¿Cuáles son los departamentos de nacimiento con mayor cantidad de egresados?

🟡 Nivel intermedio
06. **Escuelas con mayor rendimiento académico:**
¿Cuáles son las escuelas académicas con mayor promedio final?

07. **Rendimiento por modalidad:**
¿Existen diferencias en el promedio académico según la modalidad de estudio?

08. **Tiempo promedio de formación:**
¿Cuánto tiempo transcurre, en promedio, desde la primera matrícula hasta el egreso?

09. **Análisis de cohortes:**
¿Cómo se distribuyen los egresados según su año de primera matrícula?

10. **Perfil etario por escuela:**
¿Cuál es la edad promedio de los egresados de cada escuela académica?

🔴 Nivel avanzado
11. **Ranking de eficiencia académica:**
¿Qué escuelas presentan el menor tiempo promedio de formación?

12. **Análisis de cohortes:**
¿Cómo se comportan las diferentes cohortes de ingreso en términos de egreso?

13. **Segmentación de rendimiento:**
¿Cómo pueden clasificarse los egresados según su promedio final?

14. **Rendimiento por procedencia geográfica:**
¿Cuáles son las provincias cuyos egresados presentan los mayores promedios académicos?

15. **Perfil del egresado de alto rendimiento:**
¿Qué combinaciones de escuela, modalidad, sexo y procedencia geográfica presentan mayor concentración de egresados con alto rendimiento?

## Limpieza de Datos

Antes de realizar el análisis, es fundamental asegurar que los datos estén limpios y listos. Dado que las tablas `Dim_Escuela` y `Dim_Ubicacion` son de referencia, el trabajo principal se centra en la tabla `Fact_Egresados`.


1. CONTEO GENERAL DE REGISTROS 

Objetivo: Determinar el tamaño inicial de la población analizada.
```sql
SELECT COUNT(*) AS TOTAL_REGISTROS FROM Fact_Egresados; 
```

2. IDENTIFICAR DUPLICADOS POR UUID 

Objetivo: Verificar que cada egresado esté representado por un único registro.

Resultado esperado: Un UUID debería aparecer una sola vez.
```sql
SELECT UUID, COUNT(*) AS CANTIDAD_REGISTROS FROM Fact_Egresados 
GROUP BY UUID HAVING COUNT(*) > 1 ORDER BY CANTIDAD_REGISTROS DESC; 
```

3. CANTIDAD DE EGRESADOS ÚNICOS
```sql 
SELECT COUNT(DISTINCT UUID) AS EGRESADOS_UNICOS FROM Fact_Egresados;
```

4. COMPARACIÓN ENTRE REGISTROS Y EGRESADOS ÚNICOS 

Permite identificar rápidamente si existen duplicados. 
```sql
SELECT COUNT(*) AS TOTAL_REGISTROS, 
COUNT(DISTINCT UUID) AS EGRESADOS_UNICOS, 
COUNT(*) - COUNT(DISTINCT UUID) AS POSIBLES_DUPLICADOS FROM Fact_Egresados; 
```

#### Valores Nulos o Faltantes

Primero, verifiqué la existencia de valores faltantes en los dos campos clave: `EmployeeID` y `PerformanceID`. No se encontraron valores nulos.

5. PERFILAMIENTO DE VALORES NULOS

Objetivo: Identificar variables con información faltante.

```sql
SELECT SUM(CASE WHEN UUID IS NULL THEN 1 ELSE 0 END) AS UUID_NULOS, 
SUM(CASE WHEN EDAD IS NULL THEN 1 ELSE 0 END) AS EDAD_NULOS, 
SUM(CASE WHEN SEXO IS NULL THEN 1 ELSE 0 END) AS SEXO_NULOS, 
SUM(CASE WHEN COD_ESCUELA IS NULL THEN 1 ELSE 0 END) AS ESCUELA_NULOS, 
SUM(CASE WHEN MODALIDAD IS NULL THEN 1 ELSE 0 END) AS MODALIDAD_NULOS, 
SUM(CASE WHEN SEDE IS NULL THEN 1 ELSE 0 END) AS SEDE_NULOS, 
SUM(CASE WHEN UBIGEO IS NULL THEN 1 ELSE 0 END) AS UBIGEO_NULOS, 
SUM(CASE WHEN PROMEDIO_FINAL IS NULL THEN 1 ELSE 0 END) AS PROMEDIO_NULOS, 
SUM(CASE WHEN ANIO_MATRICULA1 IS NULL THEN 1 ELSE 0 END) AS ANIO_MATRICULA_NULOS, 
SUM(CASE WHEN SEMESTRE_MATRICULA1 IS NULL THEN 1 ELSE 0 END) AS SEMESTRE_MATRICULA_NULOS, 
SUM(CASE WHEN ANIO_EGRESO IS NULL THEN 1 ELSE 0 END) AS ANIO_EGRESO_NULOS, 
SUM(CASE WHEN SEMESTRE_EGRESO IS NULL THEN 1 ELSE 0 END) AS SEMESTRE_EGRESO_NULOS 
FROM Fact_Egresados;
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
    FORMAT(1.0 * COUNT(*) / SUM(COUNT(*)) OVER(),'P2') AS porcentaje
FROM Fact_Egresados
GROUP BY SEXO
```

![image](./picture/P2.png)


### Pregunta #4: Edad promedio de los egresados

A continuación.

```sql
-- Edad promedio de egresados --
SELECT 
    ROUND(AVG(EDAD),2) AS edad_promedio,
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
    ROUND(AVG(f.PROMEDIO_FINAL),2) AS promedio
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
select ROUND(AVG(
            (ANIO_EGRESO - ANIO_MATRICULA1) +
            CASE
                WHEN SEMESTRE_EGRESO = SEMESTRE_MATRICULA1 THEN 0.5
                WHEN SEMESTRE_EGRESO > SEMESTRE_MATRICULA1 THEN 1
                ELSE 0
            END
        ), 2) as prom_anios_estudio
FROM Fact_Egresados
```

### Pregunta #10: Distribución de edad por escuela académica
```sql
-- Edad promedio por escuela --
SELECT 
    e.ESCUELA_ACADEMICA,
    round(AVG(f.EDAD),1) AS edad_promedio
FROM Fact_Egresados f
JOIN Dim_Escuela e ON f.COD_ESCUELA = e.COD_ESCUELA
GROUP BY e.ESCUELA_ACADEMICA
ORDER BY edad_promedio DESC;
```

### Pregunta #11: Ranking de escuelas por eficiencia académica (tiempo de egreso)
```sql
-- Ranking de escuelas por tiempo de egreso / VERIFICAR EXACTITUD --
WITH A AS (
    SELECT 
        e.ESCUELA_ACADEMICA,
        ROUND(AVG(
            (ANIO_EGRESO - ANIO_MATRICULA1) +
            CASE
                WHEN SEMESTRE_EGRESO = SEMESTRE_MATRICULA1 THEN 0.5
                WHEN SEMESTRE_EGRESO > SEMESTRE_MATRICULA1 THEN 1
                ELSE 0
            END
        ), 2) AS tiempo_promedio
    FROM Fact_Egresados f
    JOIN Dim_Escuela e 
        ON f.COD_ESCUELA = e.COD_ESCUELA
    GROUP BY e.ESCUELA_ACADEMICA
)
SELECT 
    ESCUELA_ACADEMICA,
    tiempo_promedio,
    RANK() OVER (ORDER BY tiempo_promedio) AS ranking
FROM A;
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
    round(AVG(f.PROMEDIO_FINAL),2) AS promedio
FROM Fact_Egresados f
JOIN Dim_Ubicacion u ON f.UBIGEO = u.UBIGEO
GROUP BY u.PROVINCIA
ORDER BY promedio DESC
```

### Conclusion

- Este.


# 🎓 Análisis de Egresados UNHEVAL - Rendimiento y Trayectoria Académica

## 📌 Descripción del proyecto

Breve descripción del problema y propósito del análisis.

---

## 🎯 Objetivo de negocio

Objetivo general del proyecto.

---

## 📊 Dataset

Información general del dataset:

- Institución: Universidad Nacional Hermilio Valdizán
- Año analizado: 2024
- Unidad de análisis: Egresados de pregrado
- Variables principales:
  - Escuela académica
  - Modalidad
  - Sede
  - Sexo
  - Edad
  - Procedencia geográfica
  - Año y semestre de matrícula
  - Año y semestre de egreso
  - Promedio final

---

## 🏗️ Modelo de datos

Descripción del modelo estrella.

### Tabla de hechos

- Fact_Egresados

### Dimensiones

- Dim_Escuela
- Dim_Ubicacion
- Dim_Modalidad
- Dim_Sede
- Dim_Sexo
- Dim_Fecha

---

## ❓ Preguntas de negocio

Lista de las preguntas analíticas desarrolladas.

---

## 🔎 Análisis realizado

### Nivel básico

- Distribución de egresados por escuela.
- Distribución por sexo.
- Egresados por modalidad.
- Análisis de edad.
- Procedencia geográfica.

### Nivel intermedio

- Ranking de escuelas por rendimiento.
- Comparación de rendimiento por modalidad.
- Tiempo promedio de formación.
- Análisis de cohortes.
- Perfil etario por escuela.

### Nivel avanzado

- Ranking de eficiencia académica.
- Análisis de cohortes.
- Segmentación de rendimiento.
- Ranking geográfico.
- Perfil del egresado de alto rendimiento.

---

## 💻 Tecnologías utilizadas

- SQL
- PostgreSQL / SQL Server
- Power BI
- Excel

---

## 📈 Principales métricas

- Total de egresados
- Promedio académico
- Tiempo promedio de formación
- Ranking de escuelas
- Distribución por modalidad
- Distribución geográfica
- Cohortes de ingreso
- Segmentación de rendimiento

---

## 📂 Estructura del proyecto

Explicación breve de las carpetas.

---

## 👤 Autor

Tu nombre

LinkedIn | GitHub