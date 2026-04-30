# Investigación de las siguientes herramientas

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
