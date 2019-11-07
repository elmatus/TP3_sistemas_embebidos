# TP3 Sistemas Embebidos

# Example 1 to 9

Dado que estamos en un nuevo proyecto, debemos cambiar la configuración del debugger como se muestra a continuación:

![](https://github.com/elmatus/TP2_sistemas_embebidos/blob/master/images/debugger.PNG)

## Example 1 (Creating tasks):

Inicialmente se definen las tareas vTask1 y vTask2. Estas son muy parecidas. Lo único que varía es que una prende un led y la otra lo apaga y los mensajes enviados son distintos. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example1_task_config.PNG)

Luego, en el main, se realizan inicializaciones y se crean las tareas mediante xTaskCreate(), la cuál recibe un puntero a la función encargada de la tarea. Además con vTaskStartScheduler() se inicializa el Scheduler, el cuál es el encargado de asignar las prioridades de las tareas. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example1_main.PNG)

## Example 2 (Using the task parameter)

En este caso se tiene una única función para el manejo de tareas, la cuál hace parpadear el led. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example2_task.PNG)

Luego, en el main, se crean, al igual que en el ejemplo anterior, las dos tareas.

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example2_main.PNG)

## Example 3 (Experimenting with priorities)

Este ejemplo es similiar en gran parte al ejemplo anterior, con la modificación de prioridades en las tareas. Como se muestra en la figura, la prioridad de la tarea 1 es ´´´(tskIDLE_PRIORITY + 1UL)´´´, mientras que la de la tarea 2 es ´´´(tskIDLE_PRIORITY + 2UL)´´´. Dado que la tarea 2 tiene una mayor prioridad y estas nunca se modifican en el transcurso del programa, esta tarea se ejecutará siempre, por lo que siempre enviará el mensaje "Task 2 is running", mientras parpadea el LED3. 

![](https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/example3_vTaskCreate.PNG)
