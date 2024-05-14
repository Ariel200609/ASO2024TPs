Tiempos: sinhilos.py:

1 - 6,17s 2 - 6,16s 3 - 6,17s 4 - 6,17s 5 - 6,18s 6 - 6,22s 7 - 6,17s 8 - 6,17s 9 - 6,15s 10 - 6,18s

conhilos.py:

1 - 5,01 2 - 5,02 3 - 5,04 4 - 5,03 5 - 5,03 6 - 5,01 7 - 5,01 8 - 5,02 9 - 5,02 10 - 5,02

Respuesta Pto_1A: el principio de la ejecución de los códigos no era tan predecible,pero a medida de que los iba ajecutando nuevamente,se volvio más predecible,ya que la diferencia era de milesimas.

Respuesta Pto_1B: se comparo entre 2 compañeros ya los 2 nos dio lo mismo en ambos programas, un promedio de 5/6s en "sinhilos.py" y un promedio de 4/5s en "conhilos.py".

Respuesta Pto_1C: (sin descomentar) el código se ejecuta bien, rápido, con un promedio de 0,016Segs. (descomentado) ahora el código tarda más tiempo, un promedio de 2.45segs. se entiende que esto debio ocurrir por que el planificador de tareas tuvo algún problema o asigno mal oa destiempo los recursos de procesamiento a los hilos del programa, por eso la condición de carrera fue peor en una situación que en la otra

#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#define NUMBER_OF_THREADS 2
#define CANTIDAD_INICIAL_HAMBURGUESAS 20
int cantidad_restante_hamburguesas = CANTIDAD_INICIAL_HAMBURGUESAS;
int turno = 0;


void *comer_hamburguesa(void *tid)
{
	while (1 == 1)
	{ 
		while(turno!=(int)tid);
		
    // INICIO DE LA ZONA CRÍTICA
		if (cantidad_restante_hamburguesas > 0)
		{
			printf("Hola! soy el hilo(comensal) %d , me voy a comer una hamburguesa ! ya que todavia queda/n %d \n", (int) tid, cantidad_restante_hamburguesas);
			cantidad_restante_hamburguesas--; // me como una hamburguesa
		}
		else
		{
			printf("SE TERMINARON LAS HAMBURGUESAS :( \n");

			pthread_exit(NULL); // forzar terminacion del hilo
		}
    // SALIDA DE LA ZONA CRÍTICA   
		turno = (turno + 1)% NUMBER_OF_THREADS;


	}
}

int main(int argc, char *argv[])
{
	pthread_t threads[NUMBER_OF_THREADS];
	int status, i, ret;
	for (int i = 0; i < NUMBER_OF_THREADS; i++)
	{
		printf("Hola!, soy el hilo principal. Estoy creando el hilo %d \n", i);
		status = pthread_create(&threads[i], NULL, comer_hamburguesa, (void *)i);
		if (status != 0)
		{
			printf("Algo salio mal, al crear el hilo recibi el codigo de error %d \n", status);
			exit(-1);
		}
	}

	for (i = 0; i < NUMBER_OF_THREADS; i++)
	{
		void *retval;
		ret = pthread_join(threads[i], &retval); // espero por la terminacion de los hilos que cree
	}
	pthread_exit(NULL); // como los hilos que cree ya terminaron de ejecutarse, termino yo tambien.
}
