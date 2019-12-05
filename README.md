# TP3 Sistemas Embebidos

# Example 1 to 9

Dado que estamos en un nuevo proyecto, debemos cambiar la configuración del debugger como se muestra a continuación:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/debugger.PNG)

## Example 1 (Creating tasks):

Inicialmente se definen las tareas vTask1 y vTask2. Estas son muy parecidas. Lo único que varía es que una prende un led y la otra lo apaga y los mensajes enviados son distintos. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example1_task_config.PNG)

Luego, en el main, se realizan inicializaciones y se crean las tareas mediante xTaskCreate(), la cuál recibe un puntero a la función encargada de la tarea. Además con vTaskStartScheduler() se inicializa el Scheduler, el cuál es el encargado de asignar las prioridades de las tareas. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example1_main.PNG)

A continuación se muestra el diagrama temporal de tareas:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example1_temporal.PNG)

## Example 2 (Using the task parameter):

En este caso se tiene una única función para el manejo de tareas, la cuál hace parpadear el led. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example2_task.PNG)

Luego, en el main, se crean, al igual que en el ejemplo anterior, las dos tareas.

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example2_main.PNG)

Diagrama temporal:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example1_temporal.PNG)


## Example 3 (Experimenting with priorities):

Este ejemplo es similiar en gran parte al ejemplo anterior, con la modificación de prioridades en las tareas. Como se muestra en la figura, la prioridad de la tarea 1 es ´´´(tskIDLE_PRIORITY + 1UL)´´´, mientras que la de la tarea 2 es ´´´(tskIDLE_PRIORITY + 2UL)´´´. Dado que la tarea 2 tiene una mayor prioridad y estas nunca se modifican en el transcurso del programa, esta tarea se ejecutará siempre, por lo que siempre enviará el mensaje "Task 2 is running", mientras parpadea el LED3. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example3_vTaskCreate.PNG)

Diagrama temporal:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example3_temporal.PNG)


## Example 4 (Using the Blocked state to create delay):

En este ejemplo se implementa en la función para las tareas, vTaskFunction(), una función para realizar una demora (vTaskDelay()), a diferencia de los otros ejemplos en donde se implementó un ciclo for() para realizar la demora. La ventaja de esta función es que bloquea la tarea hasta que termine el tiempo especificado. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example4_vTaskFunction.PNG)

Diagrama temporal:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example4_temporal.PNG)

Se ve que se ejecuta la tarea 1, luego la 2 y dado que se utiliza la función vTaskDelay() que bloquea las tareas por 250ms, se entra en estado Idle por este tiempo. 

## Example 5 ():

A diferencia del ejemplo anterior se utiliza la función vTaskDelayUntil() para realizar la demora. A diferencia de vTaskDelay(), esta función realiza una demora del tiempo indicado real. Se especifica el valor absoluto de tiempo en el que queremos que la tarea se desbloquee y no importa que se realicen interrupciones en el medio de este tiempo, siempre va a contar el mismo tiempo. Con la función vTaskDelay() se especifica el tiempo en el que se quiere desbloquear una tarea relativo al tiempo en el cuál la función es llamada, lo que produce que el tiempo de bloqueo no siempre será el mismo.  

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example5_vTaskFunction.PNG)

Diagrama temporal:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example4_temporal.PNG)

# Example 10 to 16

## Example 10():

  El ejemplo 10 utiliza una cola para distribuir las tareas. La siguiente imagen muestra el diagrama de tiempo sobre este ejercicio
  
 ![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/ejercicio10.png)
 
 El ejercicio tiene 3 tareas donde la dos primeras tienen la misma prioridad mientras que la tercera tiene una prioridad mayor, y un tiempo de espera de 100 mSeg. Por la cola, la tarea de vReceiver recibe alternadamente las tareareas vSender1 y vSender2 provocando el primer tramo en el diagrama de tiempo, despues de 100 mSeg la tarea vSender1 comienza a mandar mas tareas que la tarea vSender2 provocando que el tiempo dedicaco a la tarea vSender1 es mayor que la de vSender2, despues de otros 100mSeg el tiempo de la tarea vSender1 se vuelve a agrandar mientras que la tarea vSender2 se mantiene. Hay que entender que una cola guarda la tarea recibida como una fila, y la primera tarea en entrar es la primera en salir provocando que el tiempo dedicado a cada tarea cambien cada 100 mSeg porque el vReciver espera 100mSeg para ejecutar todas las tareas.
 
 ## Example 12():

  El ejemplo 12 utiliza un semaforo para indicar a las diferentes tareas cuando deberia realizar su operacion, en este caso tenemos dos tareas Handler y Periodic, una prende y apaga el led (Handler) mientras que Periodic coloca un delay en el medio de hander con el mismo tiempo de utilizacion que Handler. El diagrama de tiempo es el acontinuación
  
  ![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/ejercicio11.png)

  Un semaforo indica a que tarea le corresponde ejecutar teniendo en cuenta que la otra tarea puede emitir el semaforo. La tarea que no esta operando se encuentra en un estado de bloqueo.


# Aplicaciones

Las aplicaciones se encuentran en el archivo TP3_sistemas_embebidos/freertos_examples_10_to_16/example/src/freertos_examples_10_to_16.c y para ejecutar cada una de ellas hay que modificar la macro TEST, como en los ejemplos anteriores. 

## Aplicación 1:

En esta aplicación se cuenta con una tarea periodica (Task1), que se ejecuta cada 500ms y la cuál es la de mayor prioridad. Esta genera una interrupción y una vez que se entra a esta interrupción se activa el semaforo, que le hace que se ejecute la tarea 2. La tarea 2 agrega un número a una cola y luego este número es leido por la tarea 3 desde la cola. 

A continuación se muestra en diagrama temporal:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/app1_temporal.PNG)
  
En la siguiente figura se muestra lo que se ve por pantalla al ejecutarse el programa:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/app1_monitor_serie.PNG)



## Aplicación 2:

En esta aplicación se cuenta con una tarea periodica (Task1), que se ejecuta cada 500ms y la cuál es la de mayor prioridad. Esta genera una interrupción y una vez que se entra a esta interrupción se activa el semaforo, que le hace que se ejecute la tarea 2. La tarea 2 agrega un número a una cola y luego este número es leido por la tarea 3 desde la cola. 

A continuación se muestra en diagrama temporal:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/app1_temporal.PNG)
  
En la siguiente figura se muestra lo que se ve por pantalla al ejecutarse el programa:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/app1_monitor_serie.PNG)








## Aplicación 3:

En esta aplicación se cuenta con tres tareas (vTask) de igual prioridad. Una vez que se ejecuta la tarea, se enciende el led por 500ms y luego se mantiene apagado por otros 500ms, y pasa a la siguiente tarea, repitiendo el proceso.
A continuación se muestra en diagrama temporal:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/app3_temporal.png)
 
Se envia por puerto serie la tarea que esta realizando, luego prende el led durante 500ms, imprimiendo por pantalla "LED encendido", y luego apaga el LED por otros 500ms, imprimiendo "LED apagado"

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/app3_vTask.png)

El programa consiste en ejecutar las tareas mediante la funcion vTaskCreate, recibiendo como parametro la tarea, el nombre de la tarea a realizar y la prioridad (las tres prioridades poseen la misma prioridad).
![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/app3_main.png)

En la siguiente figura se muestra lo que se ve por pantalla al ejecutarse el programa:

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/app3_monitor_serie.png)