# FASE 1. Investigación teórica de herramientas de diagnóstico en Linux.

Nombre: Alfonso Giménez Martínez

Curso: 1º ASIR


# EJERCICIO 1

## Investigación de las siguientes herramientas

### Inxi:

Consiste en una herramienta para el resumen general del sistema, esto incluye:CRP, RAM, discos, red y gráficos. Es un script que genera este resumen completo.

Utilidad para un técnico, es útil para hacer un primer diagnostico del equipo o para que un usuario envíe su configuración a un foro de soporte.

Ejemplo de comando: sudo inxi -Fxz

Datos clave para el informe: Kernel, CPU, driver y tarjeta de red.

### Lshw:

Consiste en una herramienta que extrae información detallada de cada componente del hardware, esto incluye (BIOS, CPU, memoria, discos, USB, PCI) desde la tabla DMI y otras fuentes.

Utilidad para un técnico, es muy precisa y útil para obtener detalles muy específicos de un componente, como la versión de la BIOS, la velocidad exacta de la RAM o la capacidad de la batería.

Ejemplo de comando: sudo lshw -short

Datos clave del informe: Fabricante y modelo de la placa base, versión de BIOS.

### Dmidecode:

Lee la tabla DMI del firmware de la placa base y la muestra en un formato legible esta tabla contiene información descriptiva y única de los componentes.

Utilidad de un técnico, es la fuente perfecta para obtener datos como el número de serie de la máquina, el UUID, el tipo de chasis o las ranuras de RAM disponibles.

Ejemplo de comando: sudo dmidecode -t system

Datos clave del informe: Número de serie, UUID del sistema.

### Lspci:

Consiste en una herramienta que lista todos los dispositivos conectados a las ranuras PCI , incluyendo gráficas, de red, de sonido, ocntroladores SATA, USB....

Utilidad de un técnico, es muy importante para indentificar el chipset de una gráfica o de una tarjeta de red, esto nos permite instalar el driver correcto en nuestro equipo.

Ejemplo de comando: lspci -n

Datos clave dle informe: Modelo de gráfica y de tarjeta de red.

### Lsusb:

Consiste en una herramienta que muestra los dispositivos conectados a los puertos USB de nuestro ordenador, por ejemplo (teclados, ratones, impresora, webcams, discos duros externos)

Utilidad de un ténico, sirve para verificar si un USB ha sido detectado por nuestro ordenador, si un dispositivo no aparece, el problema puede ser el hadrware o el kernel.

Ejemplo de comando: lsusb -t

Datos clave del informe: ID del fabricante/producto, nombre del dispositivo.

### Uname:

Consiste en una herramienta que sirve para mostrar información fundamentl del sistema operativo y el hardware de la máquina, por defecto solo imprime el nombre dle kernel.

Utilidad de un técnico, es el comando más rápido para saber que kernel y que arquitectura del procesador está utilizando nuestro ordenador, lo cual es muy importante saberlo para el tema de instalar drivers.

Ejemplo de comando: uname -a

Datos clave del informe: Versión del kernel, arquitectura.

### Lsblk:

Consiste en una herramienta que sirve para listar todos los dispositivos de bloque, como pueden ser ( discos duros, SSD, USB, particiones) mostrando sus relaciones jerárquicas en forma de árbol.

Utilidad de un técnico, permite mostrarnos para entender mejor como está particionado el disco, que tamaño tiene cada partición y en que punto del sistema de archivos está montada.

Ejemplo de comando: lsblk -f

Datos clave del informe: Nombre del disco (sda), particiones (sda1), punto de montaje (/home).

### Df:

Consiste en una herramienta que sirve para mostrar el espacio total, usado y disponible en cada sistema de archivos montados.

Utilidad de un técnico, es la herramienta principal para diagnosticar problemas de falta de espacio de disco.

Ejemplo de comando: df -hT

Datos clave del informe: Sistemas de archivos, punto de montaje.

### Free:

Consiste en una herramienta que muestra la cantidad de memoria RAM y de Swap que está libre, usada y en caché del sistema.

Utilidad de un técnico, sirve para evaluar el consumo d ememoria de los procesos, para saber si el sistema tiene suficiente RAM o si está dependiendo demasiado de la Swap, lo que haría que el equipo fluese menos fluido.

Ejemplo de comando: free -h -s 2

Datos clave del informe: RAM total, RAM disponible y swap usado.


# EJERCICIO 2

## Comprobación del estado del disco duro y de la memoria RAM.

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


# EJERCICIO 3

# Comprobación de rendimiento, temperaturas, red y estabilidad

### Lm-sensors (comando sensors):

Función principal: Detectar y mostrar la temperatura de los componentes del hardware (CPU, GPU, placa base), además de voltajes y velocidades de los ventiladores .

Aportación al técnico: Permite saber si el equipo se sobrecalienta bajo carga, lo cual es crítico en equipos antiguos con posible polvo o pasta térmica seca.

Ejemplos de comandos:

Instalación y configuración inicial (solo la primera vez)

sudo apt update && sudo apt install lm-sensors -y
sudo sensors-detect  # Responde "yes" a todas las preguntas

Ver las temperaturas: sensors

Monitorizar en tiempo real (actualiza cada 2 segundos): watch -n 2 sensors

Datos del informe en mi porpio ordenador: Temperaturas en reposo son de 35 grados y en carga he llegado hasta 85 grads (no lo he cargado demasiado).

### Htop:

Función principal: Monitor interactivo de procesos en tiempo real, versión mejorada y más colorida, muestra uso de CPU, RAM, swap y lista de procesos con su consumo.

Aportación al técnico: Identificar rápidamente qué procesos consumen más recursos (CPU o memoria) y detectar si hay procesos "zombie" o fugas de memoria.

Ejemplo de comandos:

Instalar (si no viene por defecto): sudo apt install htop -y

Ejecutar: htop

Dentro de htop: F6 para ordenar, F9 para matar un proceso, F10 para salir

Datos del informe en mi propio ordenador: Uso de mi procesaor en reposo es del 15% y eso de RAM es de 8,5Gb de 16GB.

### Stress-ng:

Función principal: Someter al sistema a situaciones de estrés controlado (CPU, memoria, disco, red) para probar su estabilidad y refrigeración.

Aportación al técnico: Permite simular cargas máximas para verificar que el sistema no se bloquee, no se reinicie y que las temperaturas se mantengan dentro de rangos seguros.

Ejemplo de comandos:

Instalar: sudo apt install stress-ng -y

Estresar 2 núcleos de CPU durante 60 segundos: stress-ng --cpu 2 --timeout 60

Prueba combinada: CPU + memoria durante 5 minutos: stress-ng --cpu 2 --vm 1 --vm-bytes 1G --timeout 300 --metrics-brief

Datos del informe en mi porpio ordenador: El sistema terminó la prueba sin bloquearse ni errores, todo parece estar correcto.

### Iperf3:

Función principal: Medir el ancho de banda máximo entre dos equipos en una red (cliente - servidor).

Aportación al técnico: Diagnostica si la tarjeta de red, el cable o el router funcionan a la velocidad esperada, muy útil para descartar cuellos de botella.

Ejemplo de comandos:

En el servidor (el que recibe la prueba): iperf3 -s

En el cliente (el que envía datos): iperf3 -c <IP_DEL_SERVIDOR>

Datos para el informe: No puedo probarlo con mi equipo, porque necesitaría un servidor.

### Ethtool:

Función principal: Consultar y modificar parámetros de las interfaces de red (velocidad negociada, duplex, estadísticas de errores).

Aportación al técnico: Verifica si la tarjeta de red está negociando la velocidad correcta (ej. 1000Mbps full duplex) o si hay errores de transmisión por mal cableado o configuración.

Ejemplo de comandos:

Ver estado de la interfaz eth0 (o ens33, enp2s0, etc.): sudo ethtool eth0

Datos para el informe: en este casono lo puedo comprobar, porque no tnego un cable de red en mi ordenador paara comprobarlo, me conecto d eforma inalámbrica a mi router.

### Ping:

Función principal: Enviar paquetes ICMP a un host remoto para medir la latencia y comprobar la conectividad básica de red.

Aportación al técnico: Comprueba si el equipo tiene salida a internet, si el DNS resuelve correctamente o si hay pérdida de paquetes.

Ejemplo de comandos:

Hacer ping al router: ping 192.168.1.1

Hacer ping a Google: ping -c 10 google.com

Datos del informe de mi ordenador: haciendo ping al router (Latencia media = 4ms / paquetes perdidos = 0)

### GParted:

Función principal: Editor gráfico de particiones permite crear, redimensionar, mover, copiar y eliminar particiones sin perder datos.

Aportación al técnico: Permite ver el estado de los discos, los sistemas de archivos y reorganizar el espacio en disco si es necesario.

Ejemplo de comandos:

Instalar: sudo apt install gparted -y

Ejecutar : sudo gparted

### HardInfo2:

Función principal: Aplicación gráfica que muestra una información muy completa del hardware y el sistema operativo.

Aportación al técnico: Ofrece una visión general rápida y muy visual, permite generar un informe HTML fácil de exportar o adjuntar a un ticket de soporte.

Ejemplo de comandos:

Instalar: sudo apt install hardinfo2 -y

Ejecutar: hardinfo2

Fuentes de información consultadas:

[https://askubuntu.com/questions/1538090/smbios-data-not-displayed-correctly-by-dmidecode-and-lshw](https://askubuntu.com/questions/1538090/smbios-data-not-displayed-correctly-by-dmidecode-and-lshw)

[https://sourceforge.net/p/clonezilla/discussion/Clonezilla_live/thread/4c57bfb1/](https://sourceforge.net/p/clonezilla/discussion/Clonezilla_live/thread/4c57bfb1/)

[https://askubuntu.com/questions/1538090


# EJERCICIO 4

### Alumno: Alfonso Giménez Martínez

### ID de equipo: Grupo 1

### Características del equipo:


| Componente                  | Marca/Fabricante                              | Modelo/Serie                | Características técnicas visibles      | Foto                                |
| ----------------------------- | ----------------------------------------------- | ----------------------------- | ------------------------------------------ | ------------------------------------- |
| **Placa base**              | Hp Engineer                                   | Compac dc7800 versión: SFF | Chipset / Socket / Nº slots RAM         | ![mb](img/placa_base.jpg)           |
| **Microprocesador**         | Intel core 2 duo E6750 266Hz                  | Core2 duo E6750 266 Hz      | (Si es visible) Modelo / Frecuencia      | ![cpu](img/cpu.jpg "CPU")           |
| **Memoria RAM**             | Fabricante: Naya                              | 667 Mhz                     | Tipo ddr2 1GB x4                         | ![ram](img/ram.jpg "RAM")           |
| **Disco HDD/SSD**           | Samsung                                       | HD 161JG3 3,5'              | Interfaz: SATA                           | ![drive](img/disco_duro.jpg)        |
| **Fuente de alimentación** | HP                                            | DPS- 240MB 100-250V         | Potencia (240), Certificación (80+): NO | ![psu](img/fuente_alimentacion.jpg) |
| **Otros (GPU/Tarjetas)**    | GPU integrada<br />Tarjeta de red: A G belcon | Dual-band wireless          | Vel.transferencia: 56mb/s                | ![otros](img/disipador.jpg)         |

### Versión de Linux instalada:

En este caso, inslamos Antix linux, ya que era la que más fluida iba, no nos dió ningún problema y tiene una interfaz muy intuitiva y fácil de usar.

Estado del disco duro:

Estado de la memoria RAM:

Comprobación de red:

Comprobación de temperaturas y estabilidad:

Incidencias detectadas:

Conclusión Final:
