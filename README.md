# TP3 Sistemas Embebidos

# Example 1 to 9

Dado que estamos en un nuevo proyecto, debemos cambiar la configuración del debugger como se muestra a continuación:

![](https://github.com/elmatus/TP2_sistemas_embebidos/blob/master/images/debugger.PNG)

## Example 1:

Inicialmente se definen las tareas vTask1 y vTask2. Estas son muy parecidas. Lo único que varía es que una prende un led y la otra lo apaga y los mensajes enviados son distintos. 

![](https://github.com/elmatus/TP2_sistemas_embebidos/blob/master/images/example1_task_config.PNG)

Luego, en el main, se realizan inicializaciones y se crean las tareas mediante xTaskCreate(), la cuál recibe un puntero a la función encargada de la tarea. Además con vTaskStartScheduler() se inicializa el Scheduler, el cuál es el encargado de asignar las prioridades de las tareas. 

![](https://github.com/elmatus/TP2_sistemas_embebidos/blob/master/images/example1_main.PNG)
