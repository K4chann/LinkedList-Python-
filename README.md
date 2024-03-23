### 📫 How to reach me:
[CALP Discord Server](https://discord.gg/JBQknmBxA9) or [send a message to K4#2381 on Discord](https://discord.com/users/349623600124526602)

### LinkedList

#### Introducción

Una LinkedList o lista encadenada es una estructurda de datos usada para
almacenar cualquier objeto en memoria. Puede parecer que haga lo mismo
que una lista simple de Python, pero tiene varias diferencias.

#### LinkedList vs Lista simple

En Python, las listas simples guardan todos sus elementos de manera que
son contiguos unos de otros en memoria. Para acceder a ellos, se usan
los índices, por lo que el acceso a sus elementos es de una complejidad
algorítmica de O(1), ya que basta con sumarle a la posición inicial de
la lista, que la tenemos, el índice del que obtener el elemento.

En las listas encadenadas esto no es posible, pues su pricipio es la no
contiguidad de sus elementos en memoria, es decir, un elemento puede
estar en Las Palmas de Gran Canaria y el siguiente en Maspalomas, hay
muchas otras cosas entre ellos, pero siempre se conectan y es posible
accederse a todos ellos.

Sus modos de acceso también difieren, pues si bien en las listas simples
no me hace falta posicionarme en ningún elemento para ir a otro, en las
listas encadenadas esto es totalmente necesario. Tengo un NODO de
comienzo, a partir del cual voy buscando el siguiente NODO y así
sucesivamente, comparable a las cintas de readiocasette, en las que la
parte visible (reproducible en el caso de las cintas) viene dada por un
puntero.

Por último, cabe destacar que dependiendo del caso de uso, un tipo de
lista puede llegar a ser mejor opción que la otra. En el caso de las
listas simples, si nuestra intención es insertar elementos entre otros y
eliminar elementos de manera muy frecuente, vamos a experimentar
retrasos en el tiempo de ejecución, pues para eliminar un elemento
distinto del final, es necesario mover todos los elementos posteriores a
él una posición hacía atrás, esto se hace para tapar los huecos entre
elementos. Por otro lado, este es el perfecto caso en el que usar
LinkedList, no es necesario reordenar los elementos al insertar o
extraer.

Sin embargo, si se quieren insertar elementos siempre al final, es mucho
mejor usar una lista simple, ya que solamente se hace un cáluclo de
direcciones con la dirección de comienzo y el tamaño de la lista. En el
caso de la LinkedList, es necesario recorrer todos y cada uno de los
elementos hasta llegar al final, aunque esto se podría solucionar
teniendo una referencia al último Nodo.

#### Estructura de una LinkedList

Este tipo de listas secuenciales tiene los siguientes elementos:

-   Nodo pricipal o primer nodo
-   Nodo final en algunas ocasiones
-   Longitud
-   Contiene Nodos, y estos son los que almacenan los valores

Como en estas listas no existe en sí los índices como se conocen en las
listas simples, cada Nodo tiene referencia a su Nodo siguiente, y en
algunas ocasiones, también a su Nodo anterior. En este caso,
desarrollaremos una lista simplemente encadenada sin Nodo final, es
decir, solo hay una conexión entre un Nodo y su siguiente, y obviamos el
Nodo final, solo poseemos el primer Nodo.

``` python
# Este código no es ejecutable
class LinkedList:

    class Node:
        def __init__(self, value, next_node = None) -> None:
            self.value = value
            self.next_node = next_node

    def __init__(self) -> None:
        self.__first = None
        self.__len = 0
    
    def __len__(self):
        return self.__len
```

Esta sería la forma báscia y general de una LinkedList. Si quisieramos
una DoubleLinkedList basta con añadir un atributo `self.__previous_node`
a la clase Node.

#### Métodos principales de las LinkedList

Sus métodos son los mismos que en las listas simples, el único cambio es
que tendremos que definirlos nosotros mismos debido a la diferencia de
acceso a sus elementos que existe entre ambas.A continuación, se
desarrollarán por separado los métodos principales
`LinkedList.append()`, `LinkedList.remove()` y `LinkedList.contains()`.

``` python
# Este código no es ejecutable
def append(self, value) -> None:
    new_node = self.Node(value)

    if len(self) == 0:
        self.__first = new_node
        
    else:
        current = self.__first

        while current.next_node is not None:
            current = current.next_node

        current.next_node = new_node
    
    self.__len += 1
```

Lo que se hace aquí es empezar desde el primer nodo avanzando hacia su
siguiente, esto siempre y cuando `next_node != None`, pues si esto no
ocurre, significaría que hemos llegado al final de la LinkedList, y como
estamos en el último Nodo, podremos insertar el nuevo valor (Nodo con
dicho valor) como su siguiente.

Si se tiene un atributo en la lista encadenada para referenciar al
último Nodo, esto sería mucho más simple:

``` python
# Este código no es ejecutable
def append(self, value) -> None:
    new_node = self.Node(value)

    if len(self) == 0:
        self.__first = self.__last = new_node
        
    else:
        self.__last.next_node = new_node
        self.__last = new_node
    
    self.__len += 1
```

[Operación
ilustrada](https://media.geeksforgeeks.org/wp-content/uploads/20240222162837/Insertion-at-the-End-of-Singly-Linked-List.webp)

Vamos a completar el código base de LinkedList planteado al principio,
resultando de la siguiente manera:

``` python
class LinkedList:

    class Node:
        def __init__(self, value, next_node = None) -> None:
            self.value = value
            self.next_node = next_node

    def __init__(self) -> None:
        self.__first = None
        self.__len = 0
    
    def __len__(self)) -> int:
        return self.__len
    
    def append(self, value) -> None:
        new_node = self.Node(value)

        if len(self) == 0:
            self.__first = new_node
            
        else:
            current = self.__first

            while current.next_node is not None:
                current = current.next_node

            current.next_node = new_node
        
        self.__len += 1

if __name__ == "__main__":
    l = LinkedList()

    for num in range(10):
        l.append(num)
    
    print("Longitud de la lista:", len(l))
```

En el caso del método remove, resultaría en el siguiente código:

 
``` python
# Este código no es ejecutable
def remove(self, value) -> None:
    if len(self) == 0:
        return
    
    if len(self) == 1:
        self.__first = None
    else:
        previous = self.__first
        current = previous.next_node

        while current is not None and previous.value != value \
                and current.value != value:
            previous = previous.next_node
            current = current.next_node
        
        if previous.value == value:
            self.__first = None
        elif current.value == value:
            previous.next_node = current.next_node \
                if current is not None else None
        else:
            return
        
        self.__len -= 1
```

Como se peude apreciar, el método para eliminar un elemento es algo más
complejo que el de insertar elementos al final. Básicamente, lo que se
está haciendo es recorrer la lista con ayuda de dos Nodos.

Se hace de esta manera para poder \"saltarse\" el Nodo que contiene el
valor a eliminar. En el momento en que `current.value == value`, es
decir, que el valor del segundo de los nodos usados para recorrer, tenga
el mismo valor que el buscado, su Nodo anterior `(previous)` tendrá como
siguiente el siguiente al Nodo encontrado `(current)`. Un simil de esto
sería pensar que construímos un puente por encima del Nodo que posee el
valor a eliminar, que conecta sus Nodos adyacentes. Se hace así para que
la referencia a dicho Nodo se pierda, y de esta manera el
`Garbage Collector` haga su trabajo eliminando el Nodo.

Aunque el método planteado no devuelve nada, podría modificarse para que
lance una excepción en caso de que el valor no se encuentre en la lista,
o devuelva un booleano para hacernos saber si el Nodo se ha podido
eliminar (está contenido en la lista) o no.

[Operación
ilustrada](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2014/05/Linkedlist_deletion.png)

Ahora tenemos los métodos mínimos necesarios para poder inicializar una
LinkedList, añadámoslo al código principal.

``` python
class LinkedList:

    class Node:
        def __init__(self, value, next_node = None) -> None:
            self.value = value
            self.next_node = next_node

    def __init__(self) -> None:
        self.__first = None
        self.__len = 0
    
    def __len__(self) -> int:
        return self.__len
    
    def append(self, value) -> None:
        new_node = self.Node(value)

        if len(self) == 0:
            self.__first = new_node
            
        else:
            current = self.__first

            while current.next_node is not None:
                current = current.next_node

            current.next_node = new_node
        
        self.__len += 1
    
    def remove(self, value) -> None:
        if len(self) == 0:
            return
        
        if len(self) == 1:
            self.__first = None
        else:
            previous = self.__first
            current = previous.next_node

            while current is not None and previous.value != value \
                    and current.value != value:
                previous = previous.next_node
                current = current.next_node
            
            if previous.value == value:
                self.__first = self.__first.next_node
            elif current.value == value:
                previous.next_node = current.next_node \
                    if current is not None else None
            else:
                return
            
        self.__len -= 1

if __name__ == "__main__":
    l = LinkedList()

    for num in range(10):
        l.append(num)

    print("Longitud al insertar 10 elementos:", len(l))

    for num in range(5):
        l.remove(num)

    print("Longitud al eliminar 5 de los elementos:", len(l))
```

```
    Longitud al insertar 10 elementos: 10
    Longitud al eliminar 5 de los elementos: 5
```
 
Por último, el método contains:

``` python
# Este código no es ejecutable
def contains(self, value) -> bool:
    current = self.__first

    while current is not None and current.value != value:
        current = current.next_node

    return current is not None
```

Este método es el más sencillo de todos, pues basta con recorrer todos
los elementos, y en caso de salir del bucle con `current != None`
significaría que el Nodo sí está contenido en la LinkedList, en caso
contrario no lo estará.

Si se quisiera usar el operador `in`, necesitaríamos sobrecargar dicho
operador, es decir, el método mágico `__contains__()`.

``` python
# Este código no es ejecutable
def __contains__(self, value) -> bool:
    return self.contains(value)
```

Probremos todos los métodos en la base del código:

``` python
class LinkedList:

    class Node:
        def __init__(self, value, next_node = None) -> None:
            self.value = value
            self.next_node = next_node
        
        def __repr__(self) -> str:
            return self.value

    def __init__(self) -> None:
        self.__first = None
        self.__len = 0
    
    def __len__(self) -> int:
        return self.__len
    
    def __contains__(self, value) -> bool:
        return self.contains(value)
    
    def append(self, value) -> None:
        new_node = self.Node(value)

        if len(self) == 0:
            self.__first = new_node
            
        else:
            current = self.__first

            while current.next_node is not None:
                current = current.next_node

            current.next_node = new_node
        
        self.__len += 1
    
    def remove(self, value) -> None:
        if len(self) == 0:
            return
        
        if len(self) == 1:
            self.__first = None
        else:
            previous = self.__first
            current = previous.next_node

            while current is not None and previous.value != value \
                    and current.value != value:
                previous = previous.next_node
                current = current.next_node
            
            if previous.value == value:
                self.__first = self.__first.next_node
            elif current.value == value:
                previous.next_node = current.next_node \
                    if current is not None else None
            else:
                return
            
        self.__len -= 1
    
    def contains(self, value) -> bool:
        current = self.__first

        while current is not None and current.value != value:
            current = current.next_node

        return current is not None

if __name__ == "__main__":
    l = LinkedList()

    for num in range(10):
        l.append(num)

    print("Longitud al insertar 10 elementos:", len(l))

    for num in range(5):
        l.remove(num)

    print("Longitud al eliminar 5 de los elementos:", len(l))

    for num in range(10):
        print(f"El valor {num} está contenido:", l.contains(num))

    print("Probando el operador IN con el valor 5:", 5 in l)
```

```
    Longitud al insertar 10 elementos: 10
    Longitud al eliminar 5 de los elementos: 5
    El valor 0 está contenido: False
    El valor 1 está contenido: False
    El valor 2 está contenido: False
    El valor 3 está contenido: False
    El valor 4 está contenido: False
    El valor 5 está contenido: True
    El valor 6 está contenido: True
    El valor 7 está contenido: True
    El valor 8 está contenido: True
    El valor 9 está contenido: True
    Probando el operador IN con el valor 5: True
```

Ahora se nos presenta un inconveniente, y es que con las listas simples
podemos imprimir en pantalla su contenido, arreglemos esto haciendo la
clase LinkedList iterable y definiendo el método mágico `__str__()`. La
hacemos iterable para además de poder recorrer sus elementos con un
bucle `for`, que el método `__string()__` pueda usar esta propiedad y
formar la string. Si tomamos el código base, resulta de la siguiente
manera:

``` python
# Este código no es ejecutable
class LinkedList:

    class Node:
        def __init__(self, value, next_node = None) -> None:
            self.value = value
            self.next_node = next_node
        
        def __str__(self) -> str:
            return self.value

    def __init__(self) -> None:
        self.__first = None
        self.__len = 0
    
    def __len__(self) -> int:
        return self.__len
    
    def __contains__(self, value) -> bool:
        return self.contains(value)
    
    def __iter__(self):
        current = self.__first

        while current is not None:
            yield current.value
            current = current.next_node
    
    def __str__(self):
        return f"[{', '.join(str(item) for item in self)}]"
```

Ahora sí que hemos formado una LinkedList completamente funcional:

``` python
class LinkedList:

    class Node:
        def __init__(self, value, next_node = None) -> None:
            self.value = value
            self.next_node = next_node
        
        def __str__(self) -> str:
            return self.value

    def __init__(self) -> None:
        self.__first = None
        self.__len = 0
    
    def __len__(self) -> int:
        return self.__len
    
    def __contains__(self, value) -> bool:
        return self.contains(value)
    
    def __iter__(self) -> any:
        current = self.__first

        while current is not None:
            yield current.value
            current = current.next_node
    
    def __str__(self) -> str:
        return f"[{', '.join(str(item) for item in self)}]"

    def append(self, value) -> None:
        new_node = self.Node(value)

        if len(self) == 0:
            self.__first = new_node
            
        else:
            current = self.__first

            while current.next_node is not None:
                current = current.next_node

            current.next_node = new_node
        
        self.__len += 1
    
    def remove(self, value) -> None:
        if len(self) == 0:
            return
        
        if len(self) == 1:
            self.__first = None
        else:
            previous = self.__first
            current = previous.next_node

            while current is not None and previous.value != value \
                    and current.value != value:
                previous = previous.next_node
                current = current.next_node
            
            if previous.value == value:
                self.__first = self.__first.next_node
            elif current.value == value:
                previous.next_node = current.next_node \
                    if current is not None else None
            else:
                return
            
        self.__len -= 1
    
    def contains(self, value) -> bool:
        current = self.__first

        while current is not None and current.value != value:
            current = current.next_node

        return current is not None

if __name__ == "__main__":
    l = LinkedList()

    for num in range(10):
        l.append(num)

    print("Longitud al insertar 10 elementos:", len(l))
    print(l)

    for num in range(5):
        l.remove(num)

    print("Longitud al eliminar 5 elementos:", len(l))
    print(l)
```

```
    Longitud al insertar 10 elementos: 10
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    Longitud al eliminar 5 elementos: 5
    [5, 6, 7, 8, 9]
```

#### Métodos avanzados

Otros métodos que se podrían desarrollar son `get()`, `ìnsert()` y
`replace()`, o la sobrecarga de operadores para conseguir el mismo
comportamiento que las listas simples mediante los métodos mágicos
`__getitem__()` y `__setitem__()`.

Empecemos por el método para optener el elemento en una determinada
posición. Aunque anteriormente se dijo que los índices no existen como
tal en las listas encadenadas, sí que se puede obtener el valor numérico
de la posición del puntero de elementos (Nodo current):

``` python
# Este código no es ejecutable
def get(self, index) -> any:
    if len(self) == 0 or index >= len(self):
        # raise IndexError("Index out of bounds")
        return

    pointer_value = 0
    current = self.__first

    while pointer_value != index:
        current = current.next_node
        pointer_value += 1

    return current.value 
```
 
Lo que se hace es simplemente recorrer los elementos de la lista y
contando los cambios de puntero que vamos haciendo. Entiéndase por
cambio de puntero por la operación `current= current.next`. Cuando el
valor númerico de dicho puntero coincida con el índice a buscar, paramos
el bucle y devolvemos el valor del elemento apuntado por el puntero.

En cuanto a los índices fuera de rango, hay dos maneras de solucionarlo,
retornando el valor None por defecto o lanzando una excepción
`IndexError`.

A continuación, se desarrolla la sobrecarga del operardor de acceso a
elementos, equivalente a `list[index]` con las listas simples.

``` python
# Este código no es ejecutable
def __getitem__(self, index) -> any:
    return self.get(index)
```
 
Por razones obvias, basta con llamar al método definido anteriormente
pasándole el índice solicitado.

Sigamos desarrollando el resto de métodos, ahora vamos con el método
`insert()`:

``` python
# Este código no es ejecutable
def insert(self, index, value) -> None:
    if len(self) == 0 or index >= len(self):
        # raise IndexError("Index out of bounds")
        return

    new_node = self.Node(value)

    if index == 0:
        new_node.next_node = self.__first
        self.__first = new_node
    else:
        pointer_value = 0
        previous = self.__first
        current = previous.next_node

        while current is not None and pointer_value < (index - 1):
            previous = previous.next_node
            current = current.next_node
        
        previous.next_node = new_node
        new_node.next_node = current
    
    self.__len += 1
```
 
[Operación
ilustrada](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist_insert_middle.png)

Al igual que en el método para obtener un elemento, se hace uso del
valor numérico del puntero para localizar la posición en la que hay que
insertar el nuevo elemento. Cuando dicho valor es igual a `index - 1`,
tendremos que situar el nuevo elemento entre el Nodo `previous` y
`current`.

Seguidamente, el método replace, que no es más que una modificación del
método `get()`, donde una vez encontrado el Nodo, se actualiza su valor:

``` python
# Este código no es ejecutable
def replace(self, index, value) -> any:
    if len(self) == 0 or index >= len(self):
        # raise IndexError("Index out of bounds")
        return

    pointer_value = 0
    current = self.__first

    while pointer_value != index:
        current = current.next_node
        pointer_value += 1
    
    current.value = value
```

[Operación
ilustrada](https://www.w3resource.com/w3r_images/java-collection-linked-list-image-exercise-26.svg)

Por último, sobrecargaremos el operador que nos permita modificar un
elemento. Para ello, simplemente llamamos a este método que acabamos de
desarrollar:

``` python
# Este código no es ejecutable
def __setitem__(self, index, value) -> None:
    return self.replace(index, value)
```

Ahora nuestra lista encadenada es mucho más avanzada, y prácticamente
tendría el mismo funcionamiento que las listas simples. El único cambio
es el modo en que se realizan sus operaciones de búsqueda, así como la
manera en la que sus elementos se buscan en memoria.

``` python
class LinkedList:

    class Node:
        def __init__(self, value, next_node = None) -> None:
            self.value = value
            self.next_node = next_node
        
        def __str__(self) -> str:
            return self.value

    def __init__(self) -> None:
        self.__first = None
        self.__len = 0
    
    def __len__(self):
        return self.__len
    
    def __contains__(self, value) -> bool:
        return self.contains(value)
    
    def __iter__(self) -> any:
        current = self.__first

        while current is not None:
            yield current.value
            current = current.next_node
    
    def __str__(self) -> str:
        return f"[{', '.join(str(item) for item in self)}]"
    
    def __getitem__(self, index) -> any:
        return self.get(index)
    
    def __setitem__(self, index, value) -> None:
        return self.replace(index, value)

    def append(self, value) -> None:
        new_node = self.Node(value)

        if len(self) == 0:
            self.__first = new_node
            
        else:
            current = self.__first

            while current.next_node is not None:
                current = current.next_node

            current.next_node = new_node
        
        self.__len += 1
    
    def remove(self, value) -> None:
        if len(self) == 0:
            return
        
        if len(self) == 1:
            self.__first = None
        else:
            previous = self.__first
            current = previous.next_node

            while current is not None and previous.value != value \
                    and current.value != value:
                previous = previous.next_node
                current = current.next_node
            
            if previous.value == value:
                self.__first = self.__first.next_node
            elif current.value == value:
                previous.next_node = current.next_node \
                    if current is not None else None
            else:
                return
            
        self.__len -= 1
    
    def contains(self, value) -> bool:
        current = self.__first

        while current is not None and current.value != value:
            current = current.next_node

        return current is not None

    def get(self, index) -> any:
        if len(self) == 0 or index >= len(self):
            # raise IndexError("Index out of bounds")
            return

        pointer_value = 0
        current = self.__first

        while pointer_value != index:
            current = current.next_node
            pointer_value += 1

        return current.value

    def insert(self, index, value) -> None:
        if len(self) == 0 or index >= len(self):
            # raise IndexError("Index out of bounds")
            return

        new_node = self.Node(value)

        if index == 0:
            new_node.next_node = self.__first
            self.__first = new_node
        else:
            pointer_value = 0
            previous = self.__first
            current = previous.next_node

            while current is not None and pointer_value < (index - 1):
                previous = previous.next_node
                current = current.next_node
            
            previous.next_node = new_node
            new_node.next_node = current
        
        self.__len += 1
    
    def replace(self, index, value) -> any:
        if len(self) == 0 or index >= len(self):
            # raise IndexError("Index out of bounds")
            return

        pointer_value = 0
        current = self.__first

        while pointer_value != index:
            current = current.next_node
            pointer_value += 1
        
        current.value = value

if __name__ == "__main__":   
    l = LinkedList()

    for num in range(10):
        l.append(num)

    print("Longitud al insertar 10 elementos:", len(l))
    print(l)

    for index in range(5):
        print(f"Elemento en la posición {index}:", l.get(index))

    for index in range(5):
        print(f"Elemento en la posición {index} mediante el operador '[]':", l[index])

    for index in range(5):
        l[index] = -1

    print("Lista tras cambiar los 5 primeros elementos a valor -1 mediante el operador '[]':", l, sep="\n")
```

```
    Longitud al insertar 10 elementos: 10
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    Elemento en la posición 0: 0
    Elemento en la posición 1: 1
    Elemento en la posición 2: 2
    Elemento en la posición 3: 3
    Elemento en la posición 4: 4
    Elemento en la posición 0 mediante el operador '[]': 0
    Elemento en la posición 1 mediante el operador '[]': 1
    Elemento en la posición 2 mediante el operador '[]': 2
    Elemento en la posición 3 mediante el operador '[]': 3
    Elemento en la posición 4 mediante el operador '[]': 4
    Lista tras cambiar los 5 primeros elementos a valor -1 mediante el operador '[]':
    [-1, -1, -1, -1, -1, 5, 6, 7, 8, 9]
```

#### Orden de los elementos

#### ¿Que pasa si necesitamos que los elementos estén ordenados?

Pues tendríamos dos opciones principales, la más eficiente que es crear
una OrderedLinkedList, cuyo funcionamiento sería idéntico a la
LinkedList desarrollada hasta ahora, pero teniendo en cuenta el orden de
los elementos a la hora se insertarlos. La segunda opción sería marcar
la iterablidad ordenada de la LinkedList, permitiéndonos así recorrarla
en orden siempre que fuera necesario. El problema de este último método
es que, el orden requerido solo sería visible a la hora de iterar sobre
la lista, y no en todo momento, pero es una opción presente.

#### Orden marcado por la función `sorted()`

Si no queremos complicarnos mucho, y solo necesitamos recorrer la lista
en orden indicado, podemos usar al función `built-in` en Python
`sorted(iterable, key=key, reverse=reverse)` de la siguiente manera.

``` python
l = LinkedList()

for num in range(9, -1, -1):
    l.append(num)

print("Antes de ordenar:", l)

l = sorted(l)

print("Después de ordenar", l)
```

```
    Antes de ordenar: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
    Después de ordenar [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
