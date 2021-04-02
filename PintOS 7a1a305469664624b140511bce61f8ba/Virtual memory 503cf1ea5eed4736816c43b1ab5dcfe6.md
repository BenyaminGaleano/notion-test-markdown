# Virtual memory

*Fase de memoria virtual*

- Estructura de los frames en la frame table

    ```c
    struct frame {
      struct list_elem elem;
      struct hash_elem helem;
      void *address;
      struct thread *owner;
    };
    ```

    Se tiene un elemento para la lista que tiene el thread sobre los frames que tiene realmente en uso **no en swap** y así a la hora de necesitar liberar recursos iterar sobre dicha lista y no sobre toda la frame table ya que esta es global y podría estar 100% ocupada.

    Se tiene un *hash elem* que es el miembro que se introduce a la hash table, **la llave de la frame table es la dirección del frame** dicha dirección es una dirección virtual kernel.

- Buscar en la frame table