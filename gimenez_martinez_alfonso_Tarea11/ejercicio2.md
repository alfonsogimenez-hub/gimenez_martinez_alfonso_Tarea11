# Comprobación del estado del disco duro y de la memoria RAM.

### Smartmontools:

Comprueba: Lee e interpreta los datos SMART del disco, realiza pruebas de diagnóstico (una cuota superficial y una larga).

Entorno de uso: Se utiliza la terminal y requiere permisos de admin.

Tipo de errores que detecta: Fallo mécanico inminente, sectores reasignados, errores de lectura/escritura, demasiado tiempo de búsqueda de datos.

Resultados en buen estado:

SMART overall-health self-assessment test result: PASSED.

Los valores de Reallocated_Sector_Ct y Current_Pending_Sector son 0.

Resultados - Problema:

SMART overall-health self-assessment test result: FAILED!.

Ejemplo de comando: sudo smartctl -a /dev/sda - sudo smartctl -t long /dev/sda

### GSmartControl:

Comprueba: Es una interfaz gráfica (GUI) que utiliza smartctl en segundo plano presenta la información SMART de forma visual y fácil de entender.

Entorno de uso: Se utiliza en entorno gráfico.

Tipo de errores que detecta: Los mismos que smartctl, pero los muestra con gráficos y códigos de color (verde = bien, rojo = mal).

Resultados - Buen Estado: Todos los atributos aparecen con un icono verde o una marca de verificación.

Resultados - Problema: Atributos marcados en rojo o con un icono de advertencia.

Ejemplo de uso: Simplemente ejecutar la aplicación desde el menú de aplicaciones, seleccionar el disco y ver la pestaña "Atributos".

### Badlocks:

Qué comprueba: Escanea la superficie del disco en busca de sectores defectuosos, escribe y lee patrones de datos para verificar la integridad de cada sector.

Entorno de uso: Se utiliza desde la terminal, es una herramienta de muy bajo nivel.

Tipo de errores que detecta:

Sectores físicamente dañados.

Sectores que han perdido la integridad de los datos.

Resultados - Buen Estado: El comando termina sin mostrar ningún número de bloque por pantalla.

Resultados - Problema: El comando imprime una lista de números de bloque, cada número es un sector defectuoso y no fiable.

Ejemplo de comando: sudo badblocks -nvs /dev/sda - sudo badblocks -wvs /dev/sda


## Herramientas pa la memoria RAM

### Memtest86+:

Qué comprueba: Realiza un análisis exhaustivo y completo de toda la memoria RAM, ejecuta una serie de complejos algoritmos de prueba (hasta 13 patrones diferentes) que escriben y leen datos en todas las direcciones de memoria.

Entorno de uso: Se ejecuta desde el arranque del equipo, sin necesidad de cargar el sistema operativo, se crea un CD, USB o se arranca desde el menú del GRUB.

Tipo de errores que detecta: Cualquier fallo físico en los chips de RAM: bits que se quedan fijos a 0 o 1, problemas de direccionamiento, fallos por calor.

Resultados - Buen Estado: La barra de progreso finaliza y en la parte inferior aparece Pass complete, no errors.

Resultados - Problema: Aparecen líneas en color rojo en la parte inferior de la pantalla con la dirección exacta del fallo y el patrón de bits que falló .

### Memtester:

Qué comprueba: Es una prueba de estrés de memoria, pero a nivel de usuario, mientras el sistema operativo está funcionando.

Entorno de uso: Se utiliza desde la terminal en un sistema Linux ya arrancado.

Tipo de errores que detecta: Errores en la memoria que está asignando al proceso, es útil para detectar fallos inducidos por calor o carga de trabajo, pero no puede probar la memoria que el sistema operativo o sus drivers están usando.

Resultados - Buen Estado: El comando termina sin errores después de las iteraciones solicitadas, mostrando un mensaje como ok.

Resultados - Problema: Muestra mensajes detallando la dirección del fallo, el valor esperado y el valor obtenido.

Ejemplo de comandos: sudo memtester 256M 5
