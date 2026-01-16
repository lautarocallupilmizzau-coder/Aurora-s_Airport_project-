✈️ README – Análisis de Operaciones Aéreas (Aerolíneas Aurora)
📌 Descripción del proyecto
Este proyecto analiza el rendimiento operativo de una aerolínea ficticia llamada Aerolíneas Aurora, utilizando tres tablas principales:

flights → información operativa de cada vuelo

costs → desglose de costes por vuelo

surveys → satisfacción del cliente

El objetivo es practicar habilidades de análisis de datos mediante SQL, explorando retrasos, costes, satisfacción y patrones operativos.
El proyecto está diseñado como un caso realista para un analista de datos junior.
📁 Aerolineas-Aurora/
│── README.md
│── 📁 data/
│     ├── flights.sql
│     ├── costs.sql
│     ├── surveys.sql
│── 📁 queries/
│     ├── basic_queries.sql
│     ├── intermediate_queries.sql
│     ├── advanced_queries.sql
│── 📁 images/
│     ├── (gráficos opcionales)
🛫 Tablas utilizadas
flights
Incluye:

fecha

origen y destino

horarios programados y reales

tipo de avión

pasajeros

costs
Incluye:

coste de combustible

coste de tripulación

tasas aeroportuarias

mantenimiento

surveys
Incluye:

rating (1 a 5)

comentario del pasajero

🎯 Objetivos del análisis
Identificar aeropuertos con mayores retrasos

Analizar el coste total por vuelo y por componente

Relacionar retrasos con satisfacción del cliente

Detectar rutas problemáticas

Evaluar el rendimiento por tipo de avión

Practicar consultas SQL de nivel básico a intermedio

SELECT 
    origin,
    AVG(TIMESTAMPDIFF(MINUTE, scheduled_departure, actual_departure)) AS retraso_promedio
FROM flights
GROUP BY origin
ORDER BY retraso_promedio DESC;

SELECT component, avg_cost
FROM (
    SELECT 'fuel_cost' AS component, AVG(fuel_cost) AS avg_cost FROM costs
    UNION ALL
    SELECT 'crew_cost', AVG(crew_cost) FROM costs
    UNION ALL
    SELECT 'airport_fees', AVG(airport_fees) FROM costs
    UNION ALL
    SELECT 'maintenance_cost', AVG(maintenance_cost) FROM costs
) AS t
ORDER BY avg_cost DESC
LIMIT 1;

SELECT flight_id, rating, comment
FROM surveys
WHERE rating < 3;

SELECT 
    f.flight_id,
    f.origin,
    f.destination,
    s.rating,
    (c.fuel_cost + c.crew_cost + c.airport_fees + c.maintenance_cost) AS total_cost
FROM flights f
JOIN costs c ON f.flight_id = c.flight_id
JOIN surveys s ON f.flight_id = s.flight_id;
📊 Insights principales (ejemplo)
MAD presenta los mayores retrasos promedio.

El componente más costoso suele ser el combustible.

Los vuelos con mayor retraso tienden a tener ratings más bajos.

Los A321 muestran más retrasos que los A319/A320.

Las rutas MAD–BCN concentran la mayor variabilidad operativa.

🛠️ Tecnologías utilizadas
MySQL Workbench

SQL (consultas básicas, joins, agregaciones)

Excel / Google Sheets

GitHub

🚀 Cómo reproducir el proyecto
Crear una base de datos en MySQL

Importar las tablas desde /data

Ejecutar las consultas desde /queries

Analizar resultados y generar visualizaciones opcionales

👤 Autor
Lautaro Callupil  
Analista de Datos Jr – Enfoque operativo‑analítico
Palma, Islas Baleares, España

📄 Licencia
Proyecto de uso libre para fines educativos y de práctica.
