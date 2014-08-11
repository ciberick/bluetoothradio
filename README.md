#Raspberry Pi Bluetooth Audio Player 
## POSSIBLE ISSUE

According to the bluez-dev team, there is an issue with the kernel (at this time Linux raspberrypi 3.6.11+)
with bluez-4.99 ([info here](http://thread.gmane.org/gmane.linux.bluez.kernel/34375)) that causes some freezing.
To cause this, successfully pair, then disconnect via the device, then attempt to reconnect...the rPi is now frozen.

If this is the case, set the proper boolean in connect.sh 

##Prerequisites:
1. Instalacion:
  * Instalar Paquetes para Bluetooh
    `sudo apt-get install bluez pulseaudio-module-bluetooth python-gobject python-gobject-2`
  * Asignamos permisos al usuario "Pi"
    `sudo usermod -a -G lp pi`
  * A continuación, vamos a hacer compatible al módulo bluetooth para la transmisión de audio. Edite /etc/bluetooth/audio.conf y agregar esto después de [General]:
    `Enable=Source,Sink,Media,Socket`
  * A continuación, vamos a hacer que PulseAudio haga reproduccion. Editar /etc/pulse/daemon.conf y elimine el comentario: **resample-method = trivial ; ADD THIS LINE TO THE FILE!**
  *Ahora Necesitamos algunos paquetes adicionales. "Qdbus" permite enviar mensajes D-Bus para el demonio de "bluez", "git-core" para poder clonar el repo, y "bluez-tools" que tiene la herramienta "bluetooth-agent" que es una de las piezas del demonio.
    `sudo apt-get install bluez-tools qdbus git-core`
  
1. Install:
  * all files in /root/bluetoothradio
  * `cp bluetoothradio/bluetooth-server /etc/init.d`
  * `chmod 755 /etc/init.d/bluetooth-server && chmod +x /etc/init.d/bluetooth-server`
  * `update-rc.d bluetooth-server defaults`
  * `reboot`
1. Requirements:
  * **/etc/bluetooth/audio.conf**
    ```[General] Enable=Source,Sink,Media,Socket```
  * **/etc/pulse/daemon.conf**
    ```resample-method = trivial```
