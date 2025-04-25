# Automatización de Recordatorio de Tareas Pendientes con n8n

Este proyecto consiste en una automatización creada con n8n para recordar tareas pendientes a través de correo electrónico, utilizando una hoja de cálculo de Google Sheets como base de datos.

## ¿Qué hace?

La automatización de n8n revisa periódicamente una hoja de cálculo de Google Sheets y envía correos electrónicos de recordatorio a los responsables de las tareas que aún no han sido marcadas como "Sí" en la columna "Terminada".

El correo electrónico incluye:

* Un saludo personalizado con el nombre del responsable.
* El nombre de la tarea pendiente.
* La fecha límite de la tarea.
* Un recordatorio para marcar la tarea como terminada.

## ¿Cómo funciona?

La automatización en n8n se basa en la lectura y procesamiento de los datos de la siguiente hoja de cálculo de Google Sheets:

| Columna        | Descripción                                                                 | Ejemplo                       |
| -------------- | --------------------------------------------------------------------------- | ----------------------------- |
| Tarea          | Descripción de la tarea pendiente.                                          | Preparar informe mensual      |
| Responsable    | Nombre de la persona responsable de la tarea.                               | Ana Pérez                   |
| Correo         | Dirección de correo electrónico del responsable.                            | ana.perez@ejemplo.com         |
| Fecha límite   | Fecha límite para completar la tarea (en formato AAAA-MM-DD o similar).     | 2025-05-05                  |
| Terminada      | Indica si la tarea está terminada ("Sí") o pendiente ("No").                | No                          |

La automatización en n8n se encarga de:

1.  **Leer los datos** de la hoja de cálculo de Google Sheets.
2.  **Filtrar las tareas** donde la columna "Terminada" sea igual a "No".
3.  Para cada tarea pendiente, **extraer el nombre del responsable, la tarea, la fecha límite y el correo electrónico**.
4.  **Enviar un correo electrónico** al responsable utilizando la plantilla proporcionada:

    ```
    Hola {{$json["Responsable"]}}, tienes tareas pendientes:

    📌 Tarea: {{$json["Tarea"]}}
    📅 Fecha límite: {{$json["Fecha límite"]}}

    ¡No olvides marcarla como terminada!
    ```

## ¿Cómo utilizar este proyecto?

1.  **Crear una hoja de cálculo en Google Sheets** con las siguientes columnas y encabezados exactamente como se indican: `Tarea`, `Responsable`, `Correo`, `Fecha límite`, `Terminada`.
2.  **Compartir la hoja de cálculo** con la integración de Google Sheets de tu instancia de n8n, dándole los permisos necesarios para leer la información.
3.  **Importar el flujo de trabajo de n8n:** El archivo adjunto (`Recordatorio_tareas_pendientes.json`) contiene el flujo de trabajo de n8n que implementa esta automatización. Para importarlo:
    * Abre tu instancia de n8n.
    * Haz clic en el botón "+" para crear un nuevo flujo de trabajo.
    * En el menú de la izquierda, busca la opción "Import" o "Import from file".
    * Selecciona el archivo `Recordatorio_tareas_pendientes.json` que has descargado.
4.  **Configurar el nodo de Google Sheets:** Una vez importado el flujo de trabajo, deberás configurar el nodo de Google Sheets para que se conecte a tu hoja de cálculo creada en el paso 1. Asegúrate de introducir el ID correcto de la hoja de cálculo.
5.  **Configurar el nodo de correo electrónico:** Configura el nodo de correo electrónico (por ejemplo, Gmail, SMTP) con tus credenciales para que n8n pueda enviar los correos de notificación.
6.  **Configurar el disparador (Trigger):** Ajusta el nodo de disparador (Trigger) en n8n para que la automatización se ejecute con la frecuencia deseada (por ejemplo, cada hora, diariamente).
7.  **Activar el flujo de trabajo:** Una vez configurado todo, activa el flujo de trabajo en n8n para que comience a funcionar.

## Archivos incluidos

* `Recordatorio_tareas_pendientes.json`:  Contiene el flujo de trabajo de n8n listo para ser importado.

## Notas

* Asegúrate de que los nombres de las columnas en tu hoja de cálculo coincidan exactamente con los especificados en este documento.
* Verifica que la integración de Google Sheets en n8n tenga los permisos necesarios para acceder a tu hoja de cálculo.
* Configura correctamente el nodo de correo electrónico para evitar problemas con el envío de notificaciones.
* Puedes personalizar la plantilla del correo electrónico en el nodo correspondiente de n8n si lo deseas.

¡Espero que esta automatización sea de gran utilidad para gestionar las tareas pendientes de tu equipo!
