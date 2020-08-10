# Redes-de-Computadores

## Prerequisitos

1. Tener python2.7 instalado

2. Descargar mininet en la branch 2.2.2 2.2.2

```
> git clone git://github.com/mininet/mininet
```

3. Descargar Pox 

```
> git clone http://github.com/noxrepo/pox
```

4. La idea es que la carpeta de pox se encuentre adentro de la carpeta de mininet

5. Poner el archivo de la topologia en la misma topos.py al mismo nivel de la carpeta mininet

6. Poner los achivos que estan en la carpeta controladores dentro de la carpeta pox/pox/forwarding, para el correcto funcionamiento de la tarea

## Red 1

### Topología

<img src="https://cdn.discordapp.com/attachments/318895169866825739/742158374895878305/unknown.png">

### Parte 1

1. Abrir dos consolas dentro de la carpeta mininet.

2. Ejecutar el comando siguiente en un consola para ejecutar el controlador de la parte 1:
```
> python2.7 pox/pox.py --verbose openflow.spanning_tree --no--flood --hold-down openflow.discorvery forwarding.l2_learning
```

3. Ejecutar el comando siguiente en la otra consola para ejecutar la consola de mininet:

```
> sudo mn --custom topos.py --topo Red1 --controller remote --switch ovsk --mac
```

4. Ejecutar el siguiente comando dentro de mininet, para ver que todos se pueden comunicar:

```
mininet> pingall
```

5. Ejecutar el siguiente comando para matar un link:

```
mininet> link s1 s2 down
```

6. Ejecutar el siguiente comando para volver a testear que todos se pueden comunicar:

```
mininet> pingall
mininet> pingall
```

7. Respondiendo a la pregunta, podemos ver que en el primer intento falla pero es porque le sirve como reconocimiento, ya que a partir del segundo funciona de pana:

### Parte 2

1. Abrir dos consolas en la carpeta mininet:

2. Ejecutar el comando siguiente para ejecutar el controlador de la parte 2:

```
python2.7 pox/pox.py --verbose openflow.spanning_tree --no-flood --hold-down openflow.discovery forwarding.circulo
```

3. Ejecutar el comando siguiente para ejecutar la consola de mininet:

```
> sudo mn --custom topos.py --topo Red1 --controller remote --switch ovsk --mac
```

4. Ejecutar el siguiente comando dentro de mininet, para ver que todos se pueden comunicar:

```
mininet> pingall
```

5. Ejecutar los siguientes comandos dentro de mininet 

   Nota: en la consola donde ejecuto el primer comando se puede visualizar los camino por los puertos, para observar que hace un sentido  antihorario.

   Estos prints tienen la siguiente estrucura:

```
mac_destino mac_fuente
vuengo de puerto
voy a otro_puerto
```
   Donde mirando la imagen de arriba pueden comprobar los caminos.

```
mininet> h1 ping h3
mininet> h1 ping h5
mininet> h3 ping h1
mininet> h3 ping h5
```

### Parte 3

1. Abrir dos consolas en la carpeta mininet

2. Ejecutar el comando siguiente para ejecutar el controlador de la parte 2:

```
python2.7 pox/pox.py --verbose openflow.spanning_tree --no-flood --hold-down openflow.discovery forwarding.xy
```

3. Ejecutar el comando siguiente para ejecutar la consola de mininet:

```
> sudo mn --custom topos.py --topo Red1 --controller remote --switch ovsk --mac
```

4. Ejecutar el siguiente comando dentro de mininet, para ver que todos se pueden comunicar:

```
mininet> pingall
```

5. Ejecutar los siguientes comandos dentro de mininet

   Nota: en la consola donde ejecuto el primer comando se puede visualizar los camino por los puertos, para observar que maximiza el uso del enlace xy.

   Estos prints tienen la siguiente estrucura:

```
mac_destino mac_fuente
vuengo de puerto
voy a otro_puerto
```
   Donde mirando la imagen de arriba pueden comprobar los caminos.

```
mininet> h1 ping h3
mininet> h1 ping h5
mininet> h3 ping h1
mininet> h3 ping h5
```

## Red 2

### Topología

<img src="https://cdn.discordapp.com/attachments/318895169866825739/742127103855689903/unknown.png">

### Comandos

1. Abrir dos consolas en la carpeta mininet

2. Ejecutar el comando siguiente para ejecutar el controlador de la parte 2

```
python2.7 pox/pox.py --verbose openflow.spanning_tree --no-flood --hold-down openflow.discovery forwarding.red2
```

3. Ejecutar el comando siguiente para ejecutar la consola de mininet

```
> sudo mn --custom topos.py --topo Red2 --controller remote --switch ovsk --mac
```

4. Ejecutar el siguiente comando dentro de mininet, para volver el host G un server 

```
mininet> g python2 -m SimpleHTTPServer 80 &
```

5. Ejecutar los siguientes comandos dentro de mininet 
   
   Nota: en la consola donde ejecuto el primer comando se puede visualizar los camino por los puertos, para observar el viaje pedido

   Estos prints tienen la siguiente estrucura:

```
mac_destino mac_fuente
vuengo de puerto
voy a otro_puerto
```
   Donde mirando la imagen de arriba pueden comprobar los caminos.

```
mininet> a wget -o - g
mininet> b wget -o - g
mininet> c wget -o - g
mininet> d wget -o - g
mininet> e wget -o - g
mininet> f wget -o - g
```

6. Ejecutar el siguiente comando, para verficiar que ping no funcionan (todo extra lo puede intentar, no permitirá nada que no sea HTTP)

```
mininet> pingall
```

