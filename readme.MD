| | |
| :-----------: | -------------: |
| ![](https://www.unirioja.es/imagenes/cabecera/cabecera_r1_c1.gif) | Metodologías avanzadas de programación para la ciencia de datos <br> Máster universitario en Ciencia de Datos y Aprendizaje Automático <br> Curso 2020 / 2021 |
| Fecha:   2 / 05 / 2021 | Nombre DIEGO POLO BENITO |


## Introducción a MPI

MPI es una API para crear y ejecutar programas paralelos. MPI esta escrita para C, C++ y Fortran. Los programas MPI se inician como un conjunto de procesos de un ejecutable, que se ejecutan de forma paralela. A medida que cada proceso se ejecuta, el programa puede necesitar intercambiar datos para combinarlos en un proceso raiz o para enviarlos a otros procesos.

El código de la práctica esta disponible en [https://github.com/dpolob/mapcd-mpi.git](https://github.com/dpolob/mapcd-mpi.git)

## Configuración
Primeramente hemos tenido que montar un clúster Beowulf. Un clúster de ordenadores conectados en una pequeña red de área local con bibliotecas y programas instalados que permiten compartir el procesamiento entre ellos.

Los programas se compilan con
`mpiCC archivo.cpp -o archivo`
y se ejecuta con
```
mpirun -machinefile archivo_de_maquinas.txt -np 4 ejecutable
mpirun -nolocal -machinefile archivo_de_maquinas.txt -np 4 ejecutable
```
archivo_de_maquinas.txt se especifican la dirección de las máquinas a utilizar.
- np:  	Numero de procesos.
- machinefile: Especifica un archivo con la dirección de las máquinas que ejecutarán el código.
- nolocal: Indica que el programa no se va a ejecutar en la máquina que lo lanza.


## Programacion con MPI

### Hello World
En este código básico se utilizan las instrucciones:
- `MPI_Comm_rank` que identifica a cada proceso
- `MPI_Comm_size` que indica el numero de procesos que hay en ejecución.
- `MPI_Init` se encarga de inicializar el entorno MPI para que se puedan comunicar los distintos procesos, por tanto debe llamarse antes de cualquier otra función MPI.
- `MPI_Finalize` que libera el entorno MPI y debe ser la ultima llamada MPI realizada.

### Send_Receive

Funcion de envío de mensaje bloqueante de un proceso de origen a uno de destino. Al ser bloqueante significa que hasta que el mensaje no haya sido enviado (que salga del buffer de salida) no se continúa la ejecución.

### Pi
En este código se ven los siguientes comandos:
- MPI_Bcast: Envía un mensaje desde un proceso origen a todos los procesos pertenecientes al mismo grupo.
- MPI_Reduce: Reduce un valor de un grupo de procesos en un único proceso raíz.

### Producto Escalar
En este código se ven los siguientes comandos:
- MPI_Scatter: Un proceso raíz trocea un mensaje en partes iguales y los envía individualmente al resto de procesos y a sí mismo.

### Multipliacion Matriz Vector
En este código se ven los siguientes comandos:
- MPI_Wtime:  toma tiempos
- MPI_Barrier: forzar un punto de sincronización o reunión de todos los procesos del comunicador.

### Merge Sort
El MergeSort es un algoritmo de ordenación fácilmente paralelizable. Este algoritmo consiste en dividir el vector a ordenar en varias partes, estas partes se ordenan y, posteriormente, se mezclan entre ellas de forma ordenada.

### Comunicadores
En este código se ven los siguientes comandos:
- MPI_Comm_split: Crea nuevos comunicadores en base a un color y una clave. Esta función particiona en subgrupos los procesos asociados al comunicador padre (comm), agrupando los procesos del mismo color en un nuevo comunicador.

### Comunicadores Cartesianos y type Vector
En este código se ven los siguientes comandos:
- MPI_Type_vector: Define un nuevo tipo de dato.
- MPI_Cart_shift: Devuelve el rango del proceso fuente y destino para una operación de movimiento en una topología cartesiana, teniendo en cuenta dirección y cantidad.

## Conclusiones
MPI permite utilizar clusters de ordenadores que corren procesos a partir de un proceso raiz. MPI dota de una serie de funciones de alto nivel para pasar parámetros y recibirlos entre los procesos lanzados.

