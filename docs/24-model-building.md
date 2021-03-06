# Construcción de modelos





## 24.2 ¿Por qué los diamantes de baja calidad son más caros? {-#diamantes-caros}

### 24.2.3 Ejercicios{-#ejercicios-2423}

1.  En el gráfico de `log_quilates` vs. `log_precio`, hay unas tiras verticales brillantes.
    ¿Qué representan?

<div class="solucion">
<h3>Solución</h3>

</div>

2.  Si `log(precio) = a_0 + a_1 * log(quilates)`, ¿Qué dice eso acerca  
    la relación entre `precio` y `quilates`?

<div class="solucion">
<h3>Solución</h3>

</div>

3.  Extrae los diamantes que tienen residuos muy altos y muy bajos. 
    ¿Hay algo inusual en estos diamantes? ¿Son particularmente malos 
    o buenos?, o ¿Crees que estos son errores de precio?

<div class="solucion">
<h3>Solución</h3>

</div>

4.  ¿El modelo final, `mod_diamantes2`, hace un buen trabajo al predecir 
    el precios de los diamantes? ¿Confiarías en lo que te indique gastar 
    si fueras a comprar un diamante?

<div class="solucion">
<h3>Solución</h3>

</div>

## 24.3 ¿Qué afecta el número de vuelos diarios?{-#vuelos-diarios}

### 24.3.5 Ejercicios{-#ejercicios-2435}

1.  Usa tus habilidades detectivescas con los buscadores para intercambiar ideas sobre por qué hubo menos vuelos esperados el 20 de enero, 26 de mayo y 1 de septiembre. (Pista: todos tienen la misma explicación.) ¿Cómo generalizarías esos días a otros años?

<div class="solucion">
<h3>Solución</h3>

</div>

2.  ¿Qué representan esos tres días con altos residuos positivos?
   ¿Cómo se generalizarían esos días a otros años?

    
    ```r
    vuelos_por_dia %>% 
      top_n(3, resid)
    ```

<div class="solucion">
<h3>Solución</h3>

</div>

3.  Crea una nueva variable que divida la variable `dia_semana` en periodos, pero sólo
    para sábados, es decir, debería tener `Thu`, `Fri`, y `Sat-verano`, 
    `Sat-primavera`, `Sat-otonio`. ¿Cómo este modelo se compara con el modelo que tiene 
    la combinación de `dia_semana` y `trimestre`?

<div class="solucion">
<h3>Solución</h3>

</div>

4.  Crea una nueva variable `dia_semana` que combina el día de la semana, periodos 
    (para sábados), y feriados públicos. ¿Cómo se ven los residuos 
    de este modelo?

<div class="solucion">
<h3>Solución</h3>

</div>

5.  ¿Qué sucede si ajustas un efecto de día de la semana que varía según el mes o varía mes a mes 
    (es decir, `n ~ dia_semana * month`)? ¿Por qué esto no es muy útil? 

<div class="solucion">
<h3>Solución</h3>

</div>

6.  ¿Que esperarías del modelo `n ~ dia_semana + ns(fecha, 5)`?
    Sabiendo lo que sabes sobre los datos, ¿porqué esperarias que no sea 
    particularmente efectivo?

<div class="solucion">
<h3>Solución</h3>

</div>

7.  Presumimos que las personas que salen los domingos son probablemente 
    viajeros de negocios quienes necesitan estar en algun lugar el lunes. Explora esa 
    hipótesis al ver cómo se descompone en función de la distancia y tiempo: si 
    es verdad, esperarías ver más vuelos en la tarde del domingo a lugares que estan muy lejos.

<div class="solucion">
<h3>Solución</h3>

</div>

8.  Es un poco frustante que el domingo y sábado esté en los extremos opuestos
    del gráfico. Escribe una pequeña función para establecer los niveles del 
    factor para que la semana comience el lunes.

<div class="solucion">
<h3>Solución</h3>

</div>

