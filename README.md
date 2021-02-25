# Práctica 1 

## 1. Identificar y describir las diferencias entre hda, sda y vda, además explicar qué significa la letra y el número al final de los identificadores

**hda**.-Es un identificador para discos duros que ocupan la interfaz IDE, el cual es un estándar de interfaces utilizado para la conexión de dispositivos de almacenamiento masivo de datos y unidades de discos ópticos que utilicen el estándar, o derivados, de ATA.

1. La letra 'a' indica que estamos localizados en el first master drive of the system, lo que nos dice que este es el disco de arranque primario. 
2. El número que le sigue al hda indica en qué partición nos encontramos. 
3. Existen tres tipos de particiones:
    1.-Primaria
    2.-Lógica
    3.-Extendida

**sda**.-Es un identificador para discos duros SCSI(Small Computer System Interface) los cuales son la interfaz que nos permite transferencia entre los buses y la computadora.

1. La 'a' nos indica que estamos localizados en el primer dispositivo SCSI. 
2. El número que le sigue al sda indica en qué partición nos encontramos. 

**vda**.-Es un identificador para discos Virtuales, en el caso de una máquina virtual. 

1. La 'a' de la misma manera nos indica que nos encontramos en el primer disco virtual. 
2. El número nos indica la partición del disco virtual. 


## 2. ¿Cómo montar y desmontar un usb en el sistema por terminal?

### Desmontar USB

Para montar/desmontar primero deberemos un dispositivo deberemos de verificar si el sistema operativo detecta un dispositivo, para eso ingresamos el comando:
```
sudo lsblk
```

El dispositivo debería aparecer como *sdb*.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso1.PNG)

Para desmontar el dispositivo ingresaremos el comando `sudo umount` más el directorio al que está montado la USB.

Para desmontar la USB en nuestro caso usaremos:
```
sudo umount /media/aaron/ESD-USB
```

Cuando desmontemos la USB al volver a ejecutar el comando `sudo lsblk` el dispositivo ya no tendrá un directorio.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso2.PNG)

### Montar USB

Para montar una USB primero debemos crear la carpeta donde se montará el dispositivo utilizando `sudo mkdir`
Nosotros la crearemos en la carpeta media, ingresando:
```
sudo mkdir /media/aaron/ESD-USB
```
Indicamos el dispositivo a montar y el directorio donde queremos que muestre su contenido.
```
sudo mount /dev/sdb1 /media/aaron/ESD-USB
```
Si el dispositivo se ha montado correctamente al ejecutar el comando `sudo ls` la USB debería aparecer con el directorio donde está montada.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso3.PNG)

## 3. Enlistar la información de los dispositivos de bloque conectados aunque no estén montados en terminal.

Para enlistar la información de los dispositivos de bloque conectados utilizamos el comando:
```
sudo lsblk
```
Si están montados aparecerán con su directorio, si no lo están aparecerán sin él.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso4.PNG)

## 4. Mostrar la tabla de particiones del disco donde está instalado el sistema operativo en terminal.

Para mostrar las particiones del disco dónde está instalado el sistema operativo podemos utilizar el comando:
```
sudo parted -l
```

Se nos desplegarán todas las particiones, su tamaño y en qué sistema de archivos está formateada.  

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso5.PNG)

## 5. Conectar una memoria usb (“usb”) y mostrar su tabla de particiones en terminal.

**Antes de comenzar con este paso deberás hacer un respaldo de la información de tu USB**

Para mostrar las particiones de la USB podemos utilizar el comando:
```
sudo parted -l
```
Se mostrará el nombre del dispositivo, sus características y su tabla de particiones.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso6.PNG)

## 6. Borrar todas las particiones del “usb” en terminal.

**Antes de borrar las particiones de una USB esta de estar desmontada usando `sudo umount`**

Para ir a la raíz del sistema ingresamos el comando:

```
sudo su
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso7.PNG)

Para visualizar la USB y su nombre ingresamos:
```
fdisk -l
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso8.PNG)

Para modificar el dispositivo USB ingresamos:
```
fdisk /dev/sdb
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso9.PNG)

Para borrar las particiones pulsamos:
```
d
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso10.PNG)

En caso de que tengamos varias particiones nos pedirá el número de partición que deseamos borrar, si sólo hay una la borrará automáticamente.
Para guardar los cambios y salir ingresamos:
```
w
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso11.PNG)

## 7. Crear en el “usb” tres particiones físicas y una extendida en terminal.
Para crear particiones nuevas en una USB deberemos utilizar el comando `fdisk` como en la sección anterior.
Para seleccionar la USB escribimos: 
```
fdisk /dev/sdb
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso12.PNG)

Para crear la primera partición física escribimos:
```
n
```

Nos indicará que tipo de partición deseamos crear, primaria ( p ) extendida ( e ) pulsamos:
```
p
```

Nos pedirá el número de partición que le deseamos asignar, como acabamos de borrar todas las particiones se le asignará 1:
```
1
```

Ahora deberemos seleccionar el punto de inicio de la partición para seleccionar el valor predeterminado pulsamos Enter.

Nos pedirá el tamaño de la partición, nosotros le daremos un tamaño de 2Gb:
```
+1G
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso12.PNG)

Para verificar la creación de la partición ingresamos:
```
p
```
Ahora crearemos 2 particiones físicas y 1 extendida.

Para crear una partición física es la siguiente cadena de comandos:

```
n
p
2
Enter
+1G
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso13.PNG)

Para la siguiente partición física:
```
n
p
3
Enter
+1G
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso14.PNG)

Y por último la para la partición extendida:
```
n
e
```

Como sólo podemos crear 4 particiones, al crear la cuarta partición de tipo extendida le asigna automáticamente el Número 4 presionamos Enter.

Para agregar todo el espacio restante a la partición presionamos Enter.

Para guardar y salir ingresamos :
```
w
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso15.PNG)

## 8. Crear una partición dentro de la partición extendida del “usb” en terminal.

Para crear una partición extendida dentro de la partición extendida que creamos anteriormente insertamos:
```
fdisk /dev/sdb
```
Para crear una nueva partición ingresamos:
```
n
```
Debido a que la USB sólo permite tener 4 particiones al momento de crear una nueva partición 5 se creará dentro de la partición extendida.

Para seleccionar el punto de inicio predeterminado presionamos Enter.

Le asignamos un tamaño:
```
+500M
```
Para guardar y salir insertamos:
```
w
```
Para salir de la raíz insertamos:
```
exit
```

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso16.PNG)

## 9. En la interfaz gráfica de la aplicación disks, borrar las particiones para que sólo exista una partición que abarque toda la “usb”.

Abrimos la aplicación Discos o Disk utility. 

Seleccionamos la USB con la que hemos estado trabajando. 

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso17.PNG)

Nos aparecerán todas las particiones actuales.

Para borrarlas, seleccionamos la partición 1 y le damos click al botón '-'.

La consola pedirá confirmación.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso18.PNG)

Hacemos el mismo proceso con las demás particiones.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso19.PNG)

Cuando nos aparezca que ya no tenemos particiones y todo sea espacio libre, se le da '+' para agregar una nueva partición. 

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso20.PNG)

Se pedirá el nuevo tamaño de la partición y se le asigna todo el espacio del dispositivo.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso21.PNG)

Se pedirá un nuevo nombre para la partición, se le puede asignar el nombre que se desee.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso22.PNG)

Al seleccionar el botón Crear se nos mostrará la nueva partición creada con el nombre que le hayamos asignado.

![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso23.PNG)


## 10. Copiar un archivo .iso de distribución live de linux a la usb por medio del comando "dd".
Antes de copiar el archivo .iso la USB deberá estar desmontada, para eso utilizamos el comando:

`sudo umount`

Agregando el directorio donde esté montada.

Para copiar un archivo de un disco a una usb, utilizaremos el comando `dd`.

Indicaremos el archivo de origen y el directorio destino:
```
sudo dd if=Descargas/ubuntu-20.04.2.0-desktop-amd64.iso of=/dev/sdb1
```
![alt text](https://github.com/19-21-29/Practica1_SO2/blob/main/Practica/Paso24.PNG)
