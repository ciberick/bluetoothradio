#Raspberry Pi Bluetooth Audio Player 

##Proceso de Instalacion:
1. Instalacion:
  * Instalar Paquetes para Bluetooh
    `sudo apt-get install bluez pulseaudio-module-bluetooth python-gobject python-gobject-2`
  * Asignamos permisos al usuario "Pi"
    `sudo usermod -a -G lp pi`
  * A continuación, vamos a hacer compatible al módulo bluetooth para la transmisión de audio. Edite **/etc/bluetooth/audio.conf** y agregar esto después de [General]:
    `Enable=Source,Sink,Media,Socket`
  * A continuación, vamos a hacer que PulseAudio haga reproduccion. Editar **/etc/pulse/daemon.conf** y elimine el comentario: `resample-method = trivial ; ADD THIS LINE TO THE FILE!**`
  * Ahora Necesitamos algunos paquetes adicionales. "Qdbus" permite enviar mensajes D-Bus para el demonio de "bluez", "git-core" para poder clonar el repo, y "bluez-tools" que tiene la herramienta "bluetooth-agent" que es una de las piezas del demonio.
    `sudo apt-get install bluez-tools qdbus git-core`

  * Ahora, vamos a la raíz, poner el siguiente código en / root:
     
    `sudo su -`

    `git clone https://github.com/ciberick/bluetoothradio --branch Wheezy`
    
    `cd bluetoothradio`
    
    `cp bluetooth-server /etc/init.d`
    
    `chmod 755 /etc/init.d/bluetooth-server && chmod +x /etc/init.d/bluetooth-server`
    
    `update-rc.d bluetooth-server defaults`
    
    `reboot`

##Uso:
Después del reinicio, ahora se puede asociar el dispositivo a través de "1234" (a menos que haya modificado el archivo bluetoothPin), y a poner su música favorita! :)

Si por alguna razón no se conecta, visite el tutorial de [KMonkey711](http://kmonkey711.blogspot.com/2012/12/a2dp-audio-on-raspberry-pi.html) y siga los pasos para conectar y asociar el dispositivo y reinicie el pi.

Otras Referencias:

[whatgeek](http://blog.whatgeek.com.pt/2014/04/20/raspberry-pi-bluetooth-wireless-speaker/)

