# struct thread

Descripción: Estructura de thread en esta fase, ver adentro para más detalles
Tags: struct

```c
struct thread
  {
    /* Owned by thread.c. */
    tid_t tid;                          /* Thread identifier. */
    enum thread_status status;          /* Thread state. */
    char name[16];                      /* Name (for debugging purposes). */
    uint8_t *stack;                     /* Saved stack pointer. */
    int priority;                       /* Priority. */
    int real_priority;                  /* Priority with donation */
    struct list_elem allelem;           /* List element for all threads list. */
    pq1714 recent_cpu;                  /* the recent cpu time in pq representation. */
    int nice;                           /* the nice value of thread. */
    struct list locks;                  /* List of locks of a thread*/
    struct lock *locked_me;             /* Pointer that references the lock who locks the current thread */
    struct thread **parent;
    bool estorbo;                       /* Boolean to know if my father is waiting on me*/
    //struct condition *cond_var;
    tid_t pid;
    
    struct semaphore *sema_parent;
    int exit_state;
    struct thread * child;
    struct thread * I;
    
    struct file *exec_file;
    void *files;                        /* Pointer to a user page that contains pointers to files opens */
    unsigned afid;                      /* available file id (sequential) */
   
    void *childsexit;

    /* Shared between thread.c and synch.c. */
    struct list_elem elem;              /* List element. */

    /* uint32_t *pagedir;                  /1* Page direction tables *1/ */

    int64_t sleep_until;

#ifdef USERPROG
    /* Owned by userprog/process.c. */
    uint32_t *pagedir;                  /* Page directory. */
#endif

    /* Owned by thread.c. */
    unsigned magic;                     /* Detects stack overflow. */
  };
```

parent es un doble puntero porque se apunta hacia el miembro I que es una referencia hacia el mismo thread, entonces cuando se libera la memoria de un thread se coloca I en null por lo que para saber si el padre esta vivo facilmente se puede consultar el valor de *parent (esto apunta hacia I que en ese momento puede o no estar en null) y verificar que esté apuntado a un thread. Por su lado childsexit (jajajaja falta ortográfica que ya no se arregló) es un puntero a una página donde la mitad de la página está reservada para almacenar los tid de los hijos y la segunda mitad (en forma de indice inverso) se almacena la información del thread con el tid asociado, mientras que files es un puntero hacia una página de memoria que almacenan los punteros de los archivos abiertos mientras que **afid** es el último indice disponible para agregar en la página,