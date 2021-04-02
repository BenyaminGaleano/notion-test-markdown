# int stdout_and_check(int fd, const void*buffer, unsigned length);

Descripción: chequea buffer y también si es stdout, si  se escribe se devuelve la cantidad de bytes escrito, sino -1 diciendo que se ha comprobado todo, pero que no se ha escrito
Tags: function