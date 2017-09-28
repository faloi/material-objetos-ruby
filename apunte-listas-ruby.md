# Listas en Ruby

## Motivación

Hay ocasiones en las cuales necesitamos que nuestros objetos puedan recordar varios elementos, por ejemplo los mensajes que recibió un celular, las cosas que tenemos que ir a comprar para el asado del Domingo o las preguntas que le vamos a hacer a una persona que estamos por entrevistar.

En todos estos casos, ocurre que no sabemos de antemano cuántos elementos vamos a tener, y por lo tanto no nos alcanza con atributos que solo puedan guardar una cosa. Veamos un ejemplo: queremos modelar un objeto `Celular` que pueda recordar los ultimos dos mensajes que recibió:

```ruby
module Kiano1100
    @cantidad_mensajes = 0

    def self.recibir_sms!(texto)
        @anteultimo_mensaje = @ultimo_mensaje
        @ultimo_mensaje = texto        
        @cantidad_mensajes += 1
    end

    def self.ultimo_mensaje
        @ultimo_mensaje
    end

    def self.anteultimo_mensaje
        @anteultimo_mensaje
    end

    def self.cantidad_mensajes
        @cantidad_mensajes
    end
end    
```

Ok, no está _taaaan_ mal. ¿Y si quisieramos recordar tres? Veamos cómo quedaría el código (esta vez, omitimos los _getters_ para facilitar la lectura):

```ruby
module Kiano1100
    @cantidad_mensajes = 0

    def self.recibir_sms!(texto)
        @antepenultimo_mensaje = @anteultimo_mensaje
        @anteultimo_mensaje = @ultimo_mensaje
        @ultimo_mensaje = texto        
        @cantidad_mensajes += 1
    end

    # acá irían los getters...
end    
```

Tuvimos que poner un tercer atributo, se va complicando un poco entender de qué se trata. :confused: ¿Y si quisieramos recordar cuatro?

```ruby
module Kiano1100
    @cantidad_mensajes = 0

    def self.recibir_sms!(texto)
        @anteantepenultimo_mensaje = @antepenultimo_mensaje
        @antepenultimo_mensaje = @anteultimo_mensaje
        @anteultimo_mensaje = @ultimo_mensaje
        @ultimo_mensaje = texto        
        @cantidad_mensajes += 1
    end

    # acá irían los getters...
end    
```

Mmm... definitivamente no es por acá, analicemos un poco lo malo de esta solución: 

* necesitamos un atributo para cada objeto que queremos guardar, lo cual hace que la cantidad de atributos crezca mucho;
* debemos conocer de antemano cuántas cosas vamos a necesitar guardar, o poner atributos de más "por las dudas";
* si nos damos cuenta que necesitamos más lugar, debemos modificar el código.

Lo que nos está faltando es algún mecanismo de poder guardar _varias_ cosas en un mismo atributo, y luego poder consultarlas. Afortunadamente, en Ruby :gem: existen unos objetos que sirven exactamente para eso, y se llaman **listas**.

Veamos de qué se tratan. :smirk:

## Características

A continuación te presentamos una versión modificada del código del celular, pero esta vez utilizando listas:

```ruby
module Kiano1100
  @mensajes = []

  def self.recibir_sms!(texto)
    @mensajes << texto 
  end

  def self.cantidad_mensajes
    @mensajes.size
  end

  def self.ultimo_mensaje
    @mensajes.last
  end  

  def self.mensajes
    @mensajes
  end
end
```

Analicemos un poco las cosas nuevas que aparecen en este código:

|Código|Explicación|
|-|-|
|`@mensajes = []`|Se crea una lista vacía, que se escribe `[]`, y se la guarda en el atributo `mensajes`.|
|`@mensajes << texto`|Se agrega el elemento `texto` a la lista `@mensajes`.|
|`@mensajes.size`|Se envía el mensaje `size` a la lista, que devuelve su tamaño.|
|`@mensajes.last`|Se envía el mensaje `last` a la lista, que devuelve el último elemento.|

Algo interesante es que para lo que antes necesitabamos un montón de atributos ahora lo podemos resolver simplemente con uno, la lista de mensajes. En Ruby, las listas vienen con un muchísimos mensajes que nos ayudan a resolver diferentes problemas. En el anexo veremos algunos de estos mensajes, pero recordá que siempre vas a poder consultar muchos más en internet - por ejemplo, en la página https://www.shortcutfoo.com/app/dojos/ruby-arrays/cheatsheet hay una lista bastante completa (qué, ufa, está en inglés :cry:).

Algunas características de las listas:

* **Tienen un orden**: no es lo mismo la lista `[Rojo, Verde, Azul]` que la lista `[Azul, Rojo, Verde]` ni `[Verde, Azul, Rojo]`.
* **Pueden contener la cantidad de elementos que querramos**: desde la lista vacía, que se escribe `[]`, hasta todos los que necesitemos.
* **Pueden modificarse**: agregando o quitando elementos, tanto al principio como al final.

## Anexo: machete de mensajes que entienden las listas

### Mensajes de acceso

|Código|Explicación|
|-|-|
|`lista.first`|Devuelve el **primer** elemento.|
|`lista.last`|Devuelve el **último** elemento.|
|`lista[3]`|Devuelve el elemento que querramos, en este caso el cuarto. El primer elemento es el 0, no el 1.|

### Mensajes para agregar

|Código|Explicación|
|-|-|
|`lista << elemento`|Agrega el elemento al final de la lista.|
|`lista.unshift(elemento)`|Agrega el elemento al principio de la lista.|
|`lista.insert(6, elemento)`|Agrega el elemento a la posición de la lista que querramos, en este caso la 6.|
|`lista.concat(lista2)`|Agrega todos los elementos de `lista2` al final de la lista.|

### Mensajes para borrar

|Código|Explicación|
|-|-|
|`lista.clear`|Borra todos los elementos de la lista.|
|`lista.pop`|Borra el último elemento de la lista.|
|`lista.shift`|Borra el primer elemento de la lista.|
|`lista.pop(5)`|Borra los últimos X elementos de la lista, en este caso 5.|
|`lista.drop(4)`|Borra los primeros X elementos de la lista, este caso 4.|
|`lista.delete(Pepita)`|Borra todos los elementos de la lista que sean iguales al parámetro, en este caso `Pepita`.|

### Mensajes para consultar

|Código|Explicación|
|-|-|
|`lista.size`|Indica cuántos elementos tiene la lista.|
|`lista.empty?`|Indica si la lista está vacía.|
|`lista.include?(Pepo)`|Indica si la lista tiene a algún elemento, en este caso `Pepo`. |

### Mensajes para transformar

|Código|Explicación|
|-|-|
|`lista.reverse`|Devuelve la lista al revés. Por ejemplo `[Agustin, Alison, Evelyn].reverse` devuelve la lista nueva `[Evelyn, Alison, Agustin]`.|
|`lista.reverse!`|Igual que el anterior, pero modifica la lista original.|
|`lista.sort`|Devuelve la lista ordenada de menor a mayor. Por ejemplo `[3, 1, 2].sort` devuelve la lista nueva `[1, 2, 3]`.|
|`lista.sort!`|Igual que el anterior, pero modifica la lista original.|
|`lista.uniq`|Devuelve la lista sin elementos repetidos. Por ejemplo `[Termo, Termo, Yerba, Mate, Yerba].uniq` devuelve la lista nueva `[Termo, Yerba, Mate]`.|
|`lista.uniq!`|Igual que el anterior, pero modifica la lista original.|

<center>
<small>
![](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)    
Material elaborado por Federico Aloi, distribuido bajo los términos de la [Licencia Creative Commons Atribución-CompartirIgual 4.0 Internacional](http://creativecommons.org/licenses/by-sa/4.0/).
</small>
</center>