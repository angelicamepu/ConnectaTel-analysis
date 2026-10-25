# 📱 Análisis de uso de clientes — ConnectaTel

Proyecto de análisis exploratorio de datos sobre el comportamiento de uso de los clientes de **ConnectaTel**, una empresa de telecomunicaciones con operaciones en México y Colombia (datos registrados hasta 2024).

## 🎯 Objetivo del proyecto

Entender cómo usan realmente los clientes los servicios móviles (llamadas y mensajes) para **optimizar la oferta comercial y mejorar la experiencia del usuario**. El análisis busca responder:

1. ¿Qué segmentos de clientes muestran mayor o menor uso de llamadas y mensajes?
2. ¿Qué usuarios presentan valores atípicos que puedan indicar comportamientos inusuales, fraude o errores de registro?
3. ¿Cómo varía el uso según la edad y el tipo de plan contratado?
4. ¿Qué patrones pueden ayudar a diseñar mejores planes y mejorar la satisfacción del cliente?

## 📂 Contenido del repositorio

```
├── ConnectaTel_Proyecto6.ipynb   # Notebook con todo el análisis
├── README.md                     # Este archivo
└── data/                         # (opcional) datasets en CSV
    ├── plans.csv
    ├── users_latam.csv
    └── usage.csv
```

> Ajusta los nombres si tus archivos se llaman distinto.

## 🗂️ Datasets utilizados

| Archivo | Descripción |
|---|---|
| `plans.csv` | Catálogo de planes: precio, minutos incluidos, GB incluidos y costo por extra. |
| `users_latam.csv` | Información de cada cliente: edad, ciudad, fecha de registro, plan contratado y fecha de baja (churn). |
| `usage.csv` | Detalle del uso real: llamadas (duración) y mensajes (longitud), con fecha y tipo de registro. |

## 🔄 Etapas del análisis

1. **Carga y exploración** de los tres datasets (`shape`, `info`, vista previa).
2. **Identificación de problemas de calidad:** nulos, valores centinela (`-999` en `age`, `"?"` en `city`) y fechas fuera de rango.
3. **Limpieza básica:** reemplazo de centinelas, conversión de fechas, marcado de fechas imposibles como nulas y revisión de nulos estructurales en `duration` y `length` (una llamada no tiene longitud y un mensaje no tiene duración).
4. **Estadísticas por usuario:** agregación de `usage` por `user_id` (mensajes, llamadas y minutos) y combinación con `users` para crear `user_profile`.
5. **Visualización y outliers:** histogramas por plan y boxplots; límites con el método IQR.
6. **Segmentación:** creación de `grupo_uso` (Bajo uso, Uso medio, Alto uso) y `grupo_edad`, visualizados con `countplot`.
7. **Insight ejecutivo:** conclusiones y recomendaciones comerciales.

## 🛠️ Herramientas

Python 3 · pandas · numpy · matplotlib · seaborn · Jupyter Notebook

## ▶️ Cómo abrir el notebook en Google Colab


O usa este botón (reemplaza `TU_USUARIO` y `TU_REPOSITORIO`):

[![Abrir en Colab](https://colab.research.google.com/drive/14gJRWwSpiMnx0p-Z3Q4xr-85kQhVf0Uc?usp=sharing)

## 🔁 Guía de reproducción



1. **Obtén los tres CSV** (`plans.csv`, `users_latam.csv`, `usage.csv`) y colócalos en la carpeta `data/` del repositorio, o súbelos a Colab.
2. **Ajusta las rutas** en la celda de carga:
   ```python
   plans = pd.read_csv("data/plans.csv")
   users = pd.read_csv("data/users_latam.csv")
   usage = pd.read_csv("data/usage.csv")
   ```
   En Colab, si subes los archivos directamente, usa solo el nombre: `pd.read_csv("plans.csv")`.
3. **Instala las dependencias** (solo si trabajas en local; Colab ya las incluye):
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
4. **Ejecuta el notebook en orden**, de arriba hacia abajo (*Runtime → Run all* en Colab o *Kernel → Restart & Run All* en Jupyter). Las celdas dependen unas de otras: por ejemplo, `user_profile` se crea en el Paso 4 y se usa en los pasos 5 y 6.

## 💡 Hallazgos principales

⚠️ **Problemas detectados en los datos**
- En la columna age habia valores de -999, identificados como sentinel, los cuales se reemplaron con la mediana
- La columna city tenía 469 valores nulos, además de ? que tambien se convirtieron a nulos
- La columna reg_date tenía fechas erróneas con 2026 y los datos usados para el análisis solo abarcan hasta el 2024
- Hubo un usuario con 0 actividad registrado

🔍 **Segmentos por Edad**
- Adulto es el segmento con mayor número de usuarios, seguido por adulto mayor, y el rango con menor uso es por parte de los jóvenes
- podrían enfocar planes para beneficiar a los adultos y adultos mayores para continuar con esa buena cuota de mercado y hacer alguna campaña para atraer la atención de los jovenes


📊 **Segmentos por Nivel de Uso**
- Uso medio concentra cerca del 73%, bajo uso cerca del 19% y alto uso solo cerca del 7%, aproximadamente
- Se debería hacer un muestreo de lo que está causando que el uso sea tan bajo para mejorar las estrategias de la empresa. 


➡️ Esto sugiere que el uso medio es el mas valioso porque es la base de los ingresos y que el que se presenta con mayor frecuencia, de la misma manera que los adultos son el público objetivo del negocio.


💡 **Recomendaciones**
- Rediseñar el plan premium, porque, al ver las gráficas, no hay ninguna diferencia que aporte una propuesta de valor que los haga más interesados en este plan, y revisar el precio.
- Crear un plan intermedio para conservar el uso medio, que es la mayoría y para la que hoy no hay una oferta pensada para este segmento
- Revisar como mejorar el alto uso y las tasas de precio de la misma
- Revisión de los datos de 130 a 155 minutos totales en las llamadas para saber si son reales o fueron errores en la toma de datos.
- Crear campañas diferenciadas por edad para atraer y retener al público objetivo. 

## 👩‍💻 Autora

**Angelica Medina** — Ingeniera ambiental y analista de datos en formación.
