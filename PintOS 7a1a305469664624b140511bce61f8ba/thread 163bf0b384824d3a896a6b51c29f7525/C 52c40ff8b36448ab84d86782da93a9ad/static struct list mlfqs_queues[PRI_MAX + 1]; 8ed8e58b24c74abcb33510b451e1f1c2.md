# static struct list mlfqs_queues[PRI_MAX + 1];

Descripción: es un array de 64 posiciones, (recuerde que PRI_MAX es 63, al sumarle uno incluimos la prioridad 0) donde cada indice representa una prioridad númera exactamente como lo establece PintOS, esta se inicializa en thread_init(void)
Tags: array, list, variable