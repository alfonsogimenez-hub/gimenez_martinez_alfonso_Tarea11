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

[https://askubuntu.com/questions/1538090](https://askubuntu.com/questions/1538090)
