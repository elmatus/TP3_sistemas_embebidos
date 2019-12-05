## Example 10 (Blocking when receiving from a queue)


En primer lugar se crean las tareas para enviar y recibir (vSenderTask y vReveiberTask). Se crearán dos tareas para enviar y una para recivir.

Luego se crea la cola XQueue, de tipo de dato xQueueHandle

(https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/ej10_1.PNG)

Entra a la función vSenderTask, donde se prende el LED3

Se verifica que haya lugar en la cola mediante xStatus. La cual recibe el dato que se va a enviar, su dirección, y el tiempo que se mantendrá bloqueado
En caso de entre en el if imprimirá un mensaje de error.
(https://github.com/elmatus/TP3_sistemas_embebidos/blob/master/images/ej10_senderTask.PNG)