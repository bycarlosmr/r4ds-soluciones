# Transformación de datos {#transform}

## Introducción


### Ejercicios

1.  Encuentra todos los vuelos que:

   1.   Tuvieron un retraso de llegada de dos o más horas
  
   2.  Volaron a Houston (`IAH` o` HOU`)
   
   3. Fueron operados por United, American o Delta
   
   4.  Partieron en verano (julio, agosto y septiembre)
   
   5.   Llegaron más de dos horas tarde, pero no salieron tarde
   
   6.  Se retrasaron por lo menos una hora, pero repusieron más de 30 minutos en vuelo
   
   7. Partieron entre la medianoche y las 6 a.m. (incluyente)

2.  Otra función de **dplyr** útil para usar filtros es `between()`. ¿Qué hace? ¿Puedes usarlo para simplificar el código necesario para responder a los desafíos anteriores?

3. ¿Cuántos vuelos tienen datos faltantes de `horario_salida`? ¿Qué otras variables tienen valores faltantes? ¿Qué representan estas filas?

4. ¿Por qué `NA ^ 0` no es faltante? ¿Por qué `NA | TRUE` no es faltante? ¿Por qué `FALSE & NA` no es faltante? ¿Puedes descubrir la regla general? (¡`NA * 0` es un contraejemplo complicado!)

## Reordenar las filas con `arrange()`


### Ejercicios

1. ¿Cómo podrías usar `arrange()` para ordenar todos los valores faltantes al comienzo? (Sugerencia: usa `is.na()`).
    
2. Ordena `vuelos` para encontrar los vuelos más retrasados. Encuentra los vuelos que salieron más temprano.

3. Ordena `vuelos` para encontrar los vuelos más rápidos.

4. ¿Cuáles vuelos viajaron más tiempo? ¿Cuál viajó menos tiempo?

## Seleccionar columnas con `select()` {#select}


### Ejercicios

1. Haz una lluvia de ideas de tantas maneras como sea posible para seleccionar `horario_salida`,` atraso_salida`,`horario_llegada`, y` atraso_llegada` de `vuelos`.

2. ¿Qué sucede si incluyes el nombre de una variable varias veces en una llamada `select()`?

3. ¿Qué hace la función `one_of()`? Por qué podría ser útil en conjunto con este vector?


```r
vars <- c ("anio", "mes", "dia", "atraso_salida", "atraso_llegada")
```

4. ¿Te sorprende el resultado de ejecutar el siguiente código? ¿Cómo tratan por defecto las funciones auxiliares de `select()` a las palabras en mayúsculas o en minúsculas? ¿Cómo puedes cambiar ese comportamiento predeterminado?


```r
select(vuelos, contains("SALIDA"))
```

## Añadir nuevas variables con `mutate()`


### Ejercicios



1. Las variables `horario_salida` y `salida_programada` tienen un formato conveniente para leer, pero es difícil realizar cualquier cálculo con ellas porque no son realmente números continuos. Transfórmalas hacia un formato más conveniente como número de minutos desde la medianoche.

2. Compara `tiempo_vuelo` con `horario_llegada - horario_salida`. ¿Qué esperas ver? ¿Qué ves? ¿Qué necesitas hacer para arreglarlo?

3. Compara `horario_salida`, `salida_programada`, y `atraso_salida`. ¿Cómo esperarías que esos tres números estén relacionados?

4. Encuentra los 10 vuelos más retrasados utilizando una función de ordenamiento. ¿Cómo quieres manejar los empates? Lee atentamente la documentación de `min_rank()`.

5. ¿Qué devuelve `1:3 + 1:10`? ¿Por qué?

6. ¿Qué funciones trigonométricas proporciona R?

## Resúmenes agrupados con `summarise()`


### Ejercicios

1.   Haz una lluvia de ideas de al menos 5 formas diferentes de evaluar las características de un retraso típico de un grupo de vuelos. Considera los siguientes escenarios:
 
    * Un vuelo llega 15 minutos antes 50% del tiempo, y 15 minutos tarde 50% del tiempo.

    * Un vuelo llega siempre 10 minutos tarde.

    * Un vuelo llega 30 minutos antes 50% del tiempo, y 30 minutos tarde 50% del tiempo.

    * Un vuelo llega a tiempo en el 99% de los casos. 1% de las veces llega 2 horas tarde.
    
    ¿Qué es más importante: retraso de la llegada o demora de salida?

2.  Sugiere un nuevo enfoque que te de el mismo *output* que `no_cancelados %>% count(destino)` y
`no_cancelado %>% count(codigo_cola, wt = distancia)` (sin usar `count()`).

3.  Nuestra definición de vuelos cancelados (`is.na(atraso_salida) | is.na (atraso_llegada)`) es un poco subóptima. ¿Por qué? ¿Cuál es la columna más importante?

4. Mira la cantidad de vuelos cancelados por día. ¿Hay un patrón? ¿La proporción de vuelos cancelados está relacionada con el retraso promedio?

5. ¿Qué compañía tiene los peores retrasos? Desafío: ¿puedes desenredar el efecto de malos aeropuertos vs. el efecto de malas aerolíneas? ¿Por qué o por qué no? (Sugerencia: piensa en `vuelos %>% group_by(aerolinea, destino) %>% summarise(n())`)

6. ¿Qué hace el argumento `sort` a `count()`. ¿Cuándo podrías usarlo?

## Transformaciones agrupadas (y filtros)


### Ejercicios

1. Remítete a las listas de funciones útiles de mutación y filtrado. Describe cómo cambia cada operación cuando las combinas con la agrupación.

2. ¿Qué avión (`codigo_cola`) tiene el peor registro de tiempo?

3. ¿A qué hora del día deberías volar si quieres evitar los retrasos lo más posible?

4. Para cada destino, calcula los minutos totales de demora. Para cada vuelo, calcula la proporción de la demora total para su destino.

5. Los retrasos suelen estar temporalmente correlacionados: incluso una vez que el problema que causó el retraso inicial se ha resuelto, los vuelos posteriores se retrasan para permitir que salgan los vuelos anteriores. Usando `lag()`, explora cómo el retraso de un vuelo está relacionado con el retraso del vuelo inmediatamente anterior.

6. Mira cada destino. ¿Puedes encontrar vuelos sospechosamente rápidos? (es decir, vuelos que representan un posible error de entrada de datos). Calcula el tiempo en el aire de un vuelo relativo al vuelo más corto a ese destino. ¿Cuáles vuelos se retrasaron más en el aire?

7. Encuentra todos los destinos que son volados por al menos dos operadores. Usa esta información para clasificar a las aerolíneas.

8. Para cada avión, cuenta el número de vuelos antes del primer retraso de más de 1 hora.