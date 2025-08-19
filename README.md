
# Análisis de reservas de hotel: Predicción de cancelaciones y optimización de ingresos

Este repositorio contiene un proyecto analítico integral centrado en el análisis de un conjunto de datos de reservas hoteleras. El objetivo principal es identificar patrones de cancelación, cuantificar su impacto financiero y desarrollar modelos predictivos que permitan mitigar pérdidas y optimizar la rentabilidad operativa.

El proyecto está implementado en Jupyter Notebook, utilzando un enfoque estructurado que combina análisis exploratorio de datos (EDA), análisis de negocio, y modelado predictivo supervisado. Los hallazgos se traducen en recomendaciones estratégicas accionables para la gestión hotelera.



## Introducción del dataset


Los datos utilizados provienen del *Hotel Reservations Classification Dataset* disponible en Kaggle, y comprenden más de 36,000 registros de reservas realizadas entre 2017 y 2018. Cada registro incluye información detallada sobre las características de la reserva, el perfil del huésped, condiciones de estancia y el estado final de la reserva (cancelada o no cancelada).

La variable objetivo principal es **`booking_status`**, una variable binaria que indica si una reserva fue cancelada. Dado que las cancelaciones representan una fuente significativa de pérdida de ingresos, este análisis se centra en comprender sus determinantes y predecirlas con anticipación.


## Variables clave analizadas


El análisis exploratorio y predictivo se basó en un conjunto de variables estratégicas, agrupadas en las siguientes categorías:

- **Variables temporales:** `lead_time`, `arrival_month`, `arrival_day_of_week`.
- **Perfil del huésped:** `repeated_guest`, `no_of_previous_cancellations`, `market_segment_type`.
- **Características de la reserva:** `avg_price_per_room`, `no_of_adults`, `no_of_children`, `no_of_special_requests`, `type_of_meal_plan`, `room_type_reserved`.
- **Condiciones operativas:** `required_car_parking_space`, `no_of_weekend_nights`, `no_of_week_nights`.

Entre todas, las variables con mayor poder predictivo identificadas fueron:

- **`lead_time`**: Número de días entre la fecha de reserva y la de llegada.
- **`avg_price_per_room`**: Precio promedio por habitación por noche.
- **`no_of_special_requests`**: Cantidad de solicitudes especiales realizadas.
- **`market_segment_type_Online`**: Canal de reserva (Online vs. Offline).
- **`repeated_guest`**: Historial de visitas previas.


## Principales hallazgos del análisis

 1. **Impacto financiero de las cancelaciones**
   - En 2018, las cancelaciones generaron pérdidas por **$4.02 millones USD**, un aumento del **149%** respecto a 2017.
   - El **36.73%** de todas las reservas en 2018 fueron canceladas, frente al 14.75% en 2017.

 2. **Patrones estacionales críticos**
   - Los meses de **junio a octubre** presentan tasas de cancelación superiores al 40%, con picos en agosto (46.55%) y octubre (46.36%).
   - Los **domingos** registran la tasa más alta de cancelación (37.34%), junto con el mayor volumen absoluto de reservas canceladas.

 3. **Perfiles de alto riesgo**
   - **Reservas anticipadas**: Cancelaciones superan el 80% cuando la reserva se realiza con más de 300 días de antelación.
   - **Grupos grandes**: Grupos de 4 personas tienen una tasa de cancelación del 43.74%.
   - **Huéspedes no recurrentes**: 33.59% de cancelación frente al 1.62% en huéspedes recurrentes.
   - **Segmento Online**: Representa el 72.4% del total de reservas y acumula el 36.51% de cancelaciones.

 4. **Relación precio-riesgo**
   - Las tarifas entre **$100 y $149** concentran el mayor volumen de cancelaciones (41.48%).
   - Las tarifas **premium (> $200)** tienen la tasa más alta (48.99%), lo que indica mayor volatilidad en el segmento de lujo.



## Acciones estratégicas propuestas

Basado en los hallazgos, se proponen las siguientes acciones para mitigar el impacto de las cancelaciones:

1. **Implementación de depósitos escalonados**
   - Aplicar depósitos no reembolsables progresivos para reservas con más de 90 días de antelación.
   - Incrementar el porcentaje de depósito para grupos grandes (4+ personas) y tarifas superiores a $100.

2. **Fortalecimiento de programas de fidelización**
   - Diseñar un programa premium para convertir huéspedes ocasionales en recurrentes, aprovechando que los huéspedes recurrentes cancelan solo en un 1.62% de los casos.
   - Ofrecer incentivos condicionados tras la primera reserva para fomentar la retención.

3. **Gestión dinámica de tarifas y overbooking**
   - Implementar ofertas de última hora para reasignar habitaciones canceladas, especialmente en temporada alta.
   - Aplicar overbooking estratégico en fines de semana y meses críticos, aprovechando las altas tasas de cancelación.

4. **Expansión del segmento corporativo**
   - Promover alianzas con empresas, dado que el segmento *Corporate* presenta una baja tasa de cancelación (10.94%).



## Modelos predictivos entrenados

Se implementaron y evaluaron dos modelos de clasificación supervisada para predecir la probabilidad de cancelación:

1. **Árbol de decisión**
2. **Random forest**

Ambos modelos fueron entrenados con validación cruzada y ajuste de hiperparámetros, priorizando el **recall** en la clase minoritaria (cancelaciones) para maximizar la detección de riesgos.

### Resultados clave

| Modelo | Accuracy | Recall (Clase 1) | Precision (Clase 1) | F1-Score (Clase 1) | AUC-ROC |
|--------|----------|------------------|----------------------|--------------------|---------|
| Árbol de Decisión | 0.81 | 0.79 | 0.73 | 0.76 | 0.85 |
| Random Forest | 0.81 | 0.79 | 0.76 | 0.77 | 0.87 |

El modelo **Random forest** mostró un rendimiento ligeramente superior, con una AUC-ROC de **0.87**, lo que indica una excelente capacidad de discriminación. Además, su naturaleza de ensamble garantiza mayor robustez frente al sobreajuste.

### Variables más influyentes
Las variables más importantes en ambos modelos fueron:
- `lead_time`
- `avg_price_per_room`
- `no_of_special_requests`
- `arrival_month`
- `market_segment_type_Online`

Esto valida los hallazgos del análisis exploratorio y refuerza su relevancia para la toma de decisiones.



## Conclusión

Este proyecto demuestra cómo el análisis de datos puede transformarse en ventaja competitiva para la industria hotelera. A través de un enfoque riguroso, se identificaron patrones críticos de comportamiento, se cuantificó el impacto financiero de las cancelaciones y se desarrolló un modelo predictivo robusto con alto potencial operativo.

La implementación de las recomendaciones propuestas podría reducir significativamente las tasas de cancelación, mejorar la previsibilidad de ingresos y optimizar la asignación de recursos.


