# Visualización de datos

## Paquetes necesarios


```r
library(ggplot2)
library(datos)
```

## Primeros pasos

### Ejercicios

1. Corre `ggplot(data = millas)`. ¿Qué observas?

2. ¿Cuántas filas hay en `millas`? ¿Cuántas columnas?

3. ¿Qué describe la variable `traccion`? Lee la ayuda de `?millas` para encontrar la respuesta.

4. Realiza un gráfico de dispersión de `autopista` versus `cilindros`.

5. ¿Qué sucede cuando haces un gráfico de dispersión de `clase` versus `traccion`? ¿Por qué no es útil este gráfico?

## Mapeos estéticos

### Ejercicios

1. ¿Qué no va bien en este código? ¿Por qué hay puntos que no son azules?

   
   ```r
   ggplot(data = millas) +
     geom_point(mapping = aes(x = motor, y = autopista, color = "blue"))
   ```
   
   <img src="03-visualize_files/figure-html/unnamed-chunk-2-1.png" width="672" />

2. ¿Qué variables en `millas` son categóricas? ¿Qué variables son continuas? (Sugerencia: escribe `?millas` para leer la documentación de ayuda para este conjunto de datos). ¿Cómo puedes ver esta información cuando ejecutas `millas`?

3. Asigna una variable continua a `color`, ` size`, y `shape`. ¿Cómo se comportan estas estéticas de manera diferente para variables categóricas y variables continuas?

4. ¿Qué ocurre si asignas o mapeas la misma variable a múltiples estéticas?

5. ¿Qué hace la estética `stroke`? ¿Con qué formas trabaja? (Sugerencia: consultar `?geom_point`)

6. ¿Qué ocurre si se asigna o mapea una estética a algo diferente del nombre de una variable, como ser `aes(color = motor < 5)`?


## Separar en facetas

### Ejercicios

1. Qué ocurre si intentas separar en facetas a una variable continua?

2. ¿Qué significan las celdas vacías que aparecen en el gráfico generado usando `facet_grid(traccion ~ cilindros)`?
¿Cómo se relacionan con este gráfico?

   
   ```r
   ggplot(data = millas) +
     geom_point(mapping = aes(x = traccion, y = cilindros))
   ```

3. ¿Qué gráfica el siguiente código? ¿Qué hace `.` ?

   
   ```r
   ggplot(data = millas) +
     geom_point(mapping = aes(x = motor, y = autopista)) +
     facet_grid(traccion ~ .)
   
   ggplot(data = millas) +
     geom_point(mapping = aes(x = motor, y = autopista)) +
     facet_grid(. ~ cilindros)
   ```

4. Mira de nuevo el primer gráfico en facetas presentado en esta sección:

   
   ```r
   ggplot(data = millas) +
     geom_point(mapping = aes(x = motor, y = autopista)) +
     facet_wrap(~ clase, nrow = 2)
   ```

   ¿Cuáles son las ventajas de separar en facetas en lugar de aplicar una estética de color?
   ¿Cuáles son las desventajas?
   ¿Cómo cambiaría este balance si tuvieras un conjunto de datos más grande?

5. Lee `?facet_wrap`. ¿Qué hace `nrow`? ¿Qué hace `ncol`?
¿Qué otras opciones controlan el diseño de los paneles individuales?
¿Por qué `facet_grid()` no tiene argumentos `nrow` y `ncol`?

6. Cuando usas `facet_grid()`, generalmente deberías poner la variable con un mayor número de niveles únicos en las columnas. ¿Por qué?

## Objetos geométricos


### Ejercicios

1. ¿Qué geom usarías para generar un gráfico de líneas?
¿Un diagrama de caja? ¿Un histograma? ¿Un gráfico de área?

2. Ejecuta este código en tu mente y predice cómo se verá el *output*.
Luego, ejecuta el código en R y verifica tus predicciones.

   
   ```r
   ggplot(data = millas, mapping = aes(x = motor, y = autopista, color = traccion)) +
     geom_point() +
     geom_smooth(se = FALSE)
   ```
3. ¿Qué muestra `show.legend = FALSE`? ¿Qué pasa si lo quitas?
 ¿Por qué crees que lo usé antes en el capítulo?

4. ¿Qué hace el argumento `se` en `geom_smooth()`?

5. ¿Se verán distintos estos gráficos? ¿Por qué sí o por qué no?

   
   ```r
   ggplot(data = millas, mapping = aes(x = motor, y = autopista)) +
     geom_point() +
     geom_smooth()
   
   ggplot() +
     geom_point(data = millas, mapping = aes(x = motor, y = autopista)) +
     geom_smooth(data = millas, mapping = aes(x = motor, y = autopista))
   ```

6. Recrea el código R necesario para generar los siguientes gráficos:

   <img src="03-visualize_files/figure-html/unnamed-chunk-8-1.png" width="50%" /><img src="03-visualize_files/figure-html/unnamed-chunk-8-2.png" width="50%" /><img src="03-visualize_files/figure-html/unnamed-chunk-8-3.png" width="50%" /><img src="03-visualize_files/figure-html/unnamed-chunk-8-4.png" width="50%" /><img src="03-visualize_files/figure-html/unnamed-chunk-8-5.png" width="50%" /><img src="03-visualize_files/figure-html/unnamed-chunk-8-6.png" width="50%" />

## Transformaciones estadísticas


### Ejercicios

1. ¿Cuál es el geom predeterminado asociado con `stat_summary()`?
¿Cómo podrías reescribir el gráfico anterior para usar esa función geom en lugar de la función stat?

2. ¿Qué hace `geom_col()`? ¿Cómo es diferente a `geom_bar()`?

3. La mayoría de los geoms y las estadísticas vienen en pares que casi siempre se usan en conjunto.
Lee la documentación y has una lista de todos los pares. ¿Qué tienen en común?

4. ¿Qué variables calcula `stat_smooth()`? ¿Qué parámetros controlan su comportamiento?

1. En nuestro gráfico de barras de proporción , necesitamos establecer `group = 1`. ¿Por qué?
En otras palabras, ¿cuál es el problema con estos dos gráficos?


   
   ```r
   ggplot(data = diamantes) +
     geom_bar(mapping = aes(x = corte, y = ..prop..))
   
   ggplot(data = diamantes) +
     geom_bar(mapping = aes(x = corte, fill = color, y = ..prop..))
   ```

## Ajustes de posición

### Ejercicios

1. ¿Cuál es el problema con este gráfico? ¿Cómo podrías mejorarlo?

   
   ```r
   ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
     geom_point()
   ```
   
   <img src="03-visualize_files/figure-html/unnamed-chunk-10-1.png" width="672" />

2. ¿Qué parámetros de `geom_jitter()` controlan la cantidad de ruido?

3. Compara y contrasta `geom_jitter()` con `geom_count()`

4. ¿Cuál es el ajuste de posición predeterminado de `geom_boxplot()`? Crea una visualización del conjunto de datos de `millas` que lo demuestre.

## Sistemas de coordenadas


### Ejercicios

1. Convierte un gráfico de barras apiladas en un gráfico circular usando `coord_polar()`.

2. ¿Qué hace `labs()`? Lee la documentación.

3. ¿Cuál es la diferencia entre `coord_quickmap()` y `coord_map()`?

4. ¿Qué te dice la gráfica siguiente sobre la relación entre la ciudad y la `autopista`? ¿Por qué es `coord_fixed()` importante? ¿Qué hace `geom_abline()`?

   
   ```r
   ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
     geom_point() +
     geom_abline() +
     coord_fixed()
   ```
   
   <img src="03-visualize_files/figure-html/unnamed-chunk-11-1.png" width="50%" />