# Práctica de listas

## Ejercicio 1: vamos de compras

### Parte A, las cosas

Vamos a modelar algunos objetos que nos van a permitir armar una lista para ir a comprar. Lo primero que representaremos son las cosas que vamos a querer comprar, de las cuales sabemos su precio, si son pesadas y si son para comer. Por ahora, tendremos:

* **Paquete de fideos:** vale 15 pesos, no es pesado, se come.
* **Tira de asado:** vale 100 pesos, es pesado, se come.
* **Esponja:** vale 7 pesos, no es pesado, no se come.
* **Termo:** vale 250 pesos, es pesado, no se come.

Creá esos objetos, asegurandote de que todos entiendan `precio`, `es_pesado?` y `se_come?`.

### Parte B, creando la lista

Ahora que ya tenemos las cosas que queremos comprar, vamos a armar la lista, que va a ser... un objeto, claro. 

Por el momento, tiene que entender los siguientes mensajes:

* `agregar!(cosa)`, que agrega la cosa a la lista;
* `proxima_cosa`, que nos devuelve el primer elemento de la lista, que es el que tenemos que comprar;
* `comprar!`, que **borra** el primer elemento de la lista, porque ya lo agarramos. _Pista:_ ojo con los dos próximos puntos, antes de borrar el elemento hay que recordarlo para poder hacerlos;
* `cosas_compradas`, que nos dice qué cosas ya compramos;
* `gasto`, que nos dice cuánto nos van a salir las cosas que ya compramos;
* `cuantas_cosas_quedan`, que nos dice cuántas cosas nos faltan comprar;
* `termine?`, que nos indica si ya compramos todo lo que había en la lista
* `falta_mucho?`, que es verdadero cuando nos faltan comprar 5 o más cosas.

<center>
    <small>
    ![](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)    
    Material elaborado por Federico Aloi, distribuido bajo los términos de la [Licencia Creative Commons Atribución-CompartirIgual 4.0 Internacional](http://creativecommons.org/licenses/by-sa/4.0/).
    </small>
</center>
