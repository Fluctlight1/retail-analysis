# Retail Analysis — Superstore

Análisis completo del dataset **Sample Superstore** con modelado dimensional en Aurora PostgreSQL, consultas SQL avanzadas y visualizaciones exploratorias.

---

## Estructura del proyecto

```
retail-analysis/
├── Retail Inteligence.ipynb   # Notebook principal
├── Data/
│   ├── Sample - Superstore.csv  # Dataset original (9,994 registros)
│   ├── DimDate.csv
│   ├── DimCustomer.csv
│   ├── DimProduct.csv
│   ├── DimLocation.csv
│   ├── DimShipMode.csv
│   └── FactSales.csv
└── Img/
    └── imagen.png             # Diagrama ERD del modelo estrella
```

---

## Contenido del notebook

### 1 · EDA
- Tipos de variables, estadísticos extendidos, distribuciones
- Reporte de missings

### 2 · Data Wrangling
- Limpieza de strings, estandarización de categorías
- Conversión de fechas, optimización de tipos (category)

### 3 · Feature Engineering
- Variables temporales: día, mes, año, trimestre, día de semana
- Métricas derivadas: `Profit_Margin`, `Revenue_Before_Discount`, `Ship_Duration`, `High_Discount_Flag`

### 4 · Modelo Estrella
Diseño dimensional con surrogate keys entero para carga en Aurora PostgreSQL.

| Tabla | Descripción |
|-------|-------------|
| `fact_sales` | 9,994 líneas de venta |
| `dim_date` | 1,434 fechas con atributos temporales |
| `dim_customer` | 793 clientes únicos |
| `dim_product` | 1,862 productos únicos |
| `dim_location` | 632 combinaciones geográficas |
| `dim_shipmode` | 4 modos de envío |

### 5 · Carga a Aurora PostgreSQL
- Schema `retail_py` en Aurora PostgreSQL 17
- Carga con `pandas.to_sql` + `engine.begin()`
- `ALTER TABLE` con PK y FK para integridad referencial

### 6 · SQL (JupySQL)
Consultas analíticas sobre el modelo estrella:

- Agregaciones y KPIs globales
- Tendencia mensual con `DATE_TRUNC`
- `RANK() OVER (PARTITION BY)` — top productos por categoría
- `LAG() OVER` — crecimiento mes a mes
- `SUM() OVER` — running total YTD
- CTE — top clientes con % de participación
- Subquery correlacionado — productos sobre el promedio de su categoría
- `CASE WHEN` — impacto de descuentos en margen

### 7 · Visualizaciones
Estilo minimalista con paleta coherente:

- Estacionalidad de ventas por año (área acumulada)
- Lollipop chart por subcategoría
- Heatmap año × mes
- Bubble chart: ventas vs margen por subcategoría
- Small multiples por año
- Violin + strip plot por segmento
- Waterfall de profit por categoría



---

## Stack

`Python` · `pandas` · `SQLAlchemy` · `psycopg2` · `matplotlib` · `JupySQL` · `scikit-learn` · `Aurora PostgreSQL 17`
