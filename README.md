# Optimizaci-n-operativa-Aeropuerto-BCNT2

### #RESUMEN: 
Este proyecto aborda uno de los mayores retos operativos de un aeropuerto: 

La gestión de la afluencia de pasajeros en las distintas zonas clave (check-in, control de seguridad, pasaportes), anticipando picos de ocupación para mejorar la planificación de recursos y reducir congestiones.Ante la ausencia de datos reales de  sensores, el proyecto combina; datos operativos de vuelos, reglas empíricas basadas en experiencia aeroportuaria y modelos de machine learning, para reconstruir, modelizar y predecir la afluencia de pasajeros en el tiempo.

-------------------------------
#### INDEX DEL PROYECTO: 
1. RECOGIDA DE DATOS : (notebook 1, 2, 3 y 4)
2. Limpieza y la variable Aircraft (notebook 5, 6, 7, 8, 9, 10, 11) + (notebook 12 limpieza de datos internos de ocupación 1 día) + (notebook 13 limpieza de datos internos de ocupación)
3. Modelo de ocupación (notebook 14 y 15)
4. limpieza de clima (notebook 16)
5. DIstribución y conversion a tabla por horas (notebook 17)
6. Modelo de afluencia (notebook 18,19,20)
Para una mayor privacidad se limita la visualización de datos del notebook 12 y 13 en el cual se trabaja con datos internos.
-------------------------------
#### OBJETIVO: 
Reconstruir la afluencia real de pasajeros por zona aeroportuaria.

- Predecir la ocupación del resto de vuelos, a través de datos internos para conocer los pasajeros de cada vuelo. 
- Predecir la afluencia por zonas y horas en el Aeropuerto de BCN-T2
- Visualizar resultados de forma intuitiva mediante Streamlit y mapas interactivos.

#### PROCEDIMIENTO: 
METOLOGÍA para convertir tabla en horas: Expansión temporal a nivel minuto:
- Los datos originales están agregados por vuelo y hora de salida.
- Para ganar precisión: Se define un intervalo operativo por vuelo (apertura y cierre) y se expande cada vuelo a múltiples filas por minuto usando pd.date_range(freq="1min").Cada vuelo pasa a representarse como una distribución temporal continua.

#### Asignación ponderada por tramos:
Cada intervalo se divide en tramos temporales, representando patrones reales de llegada de pasajeros.
Ejemplo en Check-in:
- Tramo 1: llegada temprana
- Tramo 2: llegada tardía

#### Selección de pasajeros que entran al sistema: No todos los pasajeros pasan por todas las zonas: 
- Se define un porcentaje de pasajeros que NO pasan por check-in, distinto por tipo de vuelo.
- Conservación de masa: Tras la distribución: Se valida que la suma de pasajeros por vuelo coincide con el total original. Para garantizar que ningún pasajero desaparece artificialmente se aplica un factor de normalización para corregir errores numéricos acumulados.

#### Modelado predictivo: 
Se entrenan 3 modelos para predecir la afluencia en cada zona: Series temporales con Random forest. Métricas usadas:(R²,RMSE) Se trabaja en un entorno concreto, el mismo que en streamlit. 

#### Visualización e interfaz:
El proyecto incluye una aplicación Streamlit con: KPIs diarios por zona, gráficos históricos por horas, días y semanas, mapa interactivo (Folium). Esto permite: análisis histórico, toma de decisiones visual e intuitiva.
