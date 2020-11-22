# Configuracion_Proyecto_Redes
Manual de configuración de la topología 2 del proyecto del curso Redes de computadoras 1 

## Descripcion

En la topologia #2 nos encontramos con 4 diferentes equipos de distintos sistemas operativos, los cuales 2 de ellos se encuentran en una vlan y 2 en otra, la distribucion de las redes cuenta con la implementacion de protocolos de redundancia activo pasivo a demas de enrutamiento dinamico y configuracion de vtp para el manejo de las vlans.  

Esta topologia se conecta a una distinta mediante la nube. 


## Topologia

La Tolopogia numero 2 consiste en una seria de modificaciones, las cuales se detallan mas adelante.

![image](https://user-images.githubusercontent.com/37676214/99899607-445f7d00-2c70-11eb-9ab8-68dca8c6b798.png)

## Configuraciones

### VTP

![image](https://user-images.githubusercontent.com/37676214/99900031-365f2b80-2c73-11eb-9898-c4da8c81e6c4.png)

![image](https://user-images.githubusercontent.com/37676214/99900035-3eb76680-2c73-11eb-8ce4-6d1a46febccc.png)

![image](https://user-images.githubusercontent.com/37676214/99900040-470fa180-2c73-11eb-8492-c4d63aceb51d.png)


### VLANS

![image](https://user-images.githubusercontent.com/37676214/99900190-e03eb800-2c73-11eb-8139-bf02d7c323e8.png)

#### Configuraciones individuales de las VLANS en ESW# 

##### ESW1
```sh
!
interface Vlan77
 ip address 70.0.77.253 255.255.255.0
 standby 1 ip 70.0.77.251
 standby 1 priority 75
 standby 1 preempt
!         
interface Vlan87
 ip address 70.0.87.253 255.255.255.0
 standby 2 ip 70.0.87.251
 standby 2 priority 75
 standby 2 preempt
!
```

##### ESW2
```sh
!
interface Vlan77
 ip address 70.0.77.254 255.255.255.0
 standby 1 ip 70.0.77.251
 standby 1 preempt
!         
interface Vlan87
 ip address 70.0.87.254 255.255.255.0
 standby 2 ip 70.0.87.251
 standby 2 preempt
!
```

##### ESW3
```sh
!
interface Vlan77
 ip address 70.0.77.252 255.255.255.0
 standby 1 ip 70.0.77.251
 standby 1 priority 50
 standby 1 preempt
!
interface Vlan87
 ip address 70.0.87.252 255.255.255.0
 standby 2 ip 70.0.87.251
 standby 2 priority 50
 standby 2 preempt
!
```

### HSRP

![image](https://user-images.githubusercontent.com/37676214/99900266-26941700-2c74-11eb-9c80-d5da19d0d4b8.png)

![image](https://user-images.githubusercontent.com/37676214/99900273-327fd900-2c74-11eb-9417-abb0b34a6cd8.png)

![image](https://user-images.githubusercontent.com/37676214/99900281-3d3a6e00-2c74-11eb-86b8-5eda8bc48753.png)

### EIGRP

El protocolo EIGRP se encuentra modificado de la siguiente manera de forma individual en cada uno de los dispositivos.

#### ESW1
```sh
!
router eigrp 555
 network 6.0.0.0
 no auto-summary
!
```

#### ESW2
```sh
!
router eigrp 555
 network 7.0.0.0
 network 70.0.77.0 0.0.0.255
 network 70.0.87.0 0.0.0.255
 no auto-summary
!
```

#### ESW3
```sh
!
router eigrp 555
 network 8.0.0.0
 no auto-summary
!
```

#### R1

```sh
!
router eigrp 555
 network 6.0.0.0
 network 7.0.0.0
 network 8.0.0.0
 no auto-summary
!
```

## Capturas de Paquetes

Se capturaron paquetes en la interfaz activa con un ping desde una maquina en la vlan 77 hacia R1.

![image](https://user-images.githubusercontent.com/37676214/99899927-5e01c400-2c72-11eb-811c-419bc8de6557.png)

Se pueden notar los paquetes de ICMP como tambien los paquetes 'HELLO' enviados por el protocolo eigrp para verificar que la conexion no se haya perdido. 

## Manual de comandos

Las configuraciones para los distintos equipos se hicieron en base a los siguientes procedimientos:

### Configurar interface de switch en modo trunk

```sh 
SW1 > enable
SW1#configure terminal
SW1(config)#interface fastethernet #/#
SW1(config-if)#switchport mode trunk
SW1(config-if)#exit
```

### Configurar interface de switch en modo acceso

```sh 
SW1 > enable
SW1#configure terminal
SW1(config)#interface fastethernet #/#
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan #
SW1(config-if)#exit
```

### Creacion de una VLAN

```sh 
SW1 > enable
SW1#configure terminal 
SW1(config)#vlan # 
SW1(config-vlan)#name [nombre] 
SW1(config-vlan)#exit
```

### Eliminacion de una VLAN

```sh
SW1 > enable
SW1#configure terminal 
SW1(config)#no vlan #
SW1(config)#exit
```


### Configuracion de VTP

```sh
SW1 > enable
SW1#configure terminal 
Switch(config)#vtp mode [Modo]
Switch(config)#vtp domain cisco [dominio]
Switch(config)#vtp password cisco [password]
SW1(config)#exit
```

### Enrutamiento Dinamico

#### RIP

```sh
SW1 > enable 
SW1#configure terminal 
SW1(config)#route rip 
SW1(config-router)#network [direccion de la red que queremos propagar]
SW1(config-router)#no auto-summary
SW1(config-router)#exit
```

#### OSPF

```sh 
SW1 > enable 
SW1#configure terminal 
SW1(config)#route ospf [id del proceso]
SW1(config-router)#network [direccion de la red que queremos propagar] [wildcard | mascara de subred en complemento] area [num]
SW1(config-router)#exit
```

#### EIGRP

```sh 
SW1 > enable 
SW1#configure terminal 
SW1(config)#router eigrp [id del sistema autonomo]
SW1(config-router)#network [direcciones ip de las redes que quiero replicar] [mascara de subred en complemento]
SW1(config-router)#no auto-summary
SW1(config-router)#exit
```

### Enrutamiento Estatico

```sh 
SW1>enable
SW1#configure terminal 
SW1(config)#ip route [dirección-red] [mascara-SubRed] {dirección próximo salto}
SW1(config)#exit
```

### Protocolo de Redundancia Activo/Pasivo HSRP
 
```sh 
R1>enable
R1#configure terminal 
R1(config)# interface [tipo-Interfaz] #/# 
R1(config-if)# standby [numero de grupo] ip [ip-virtual] 
R1(config-if)# standby # priority # 
R1(config-if)# standby # preempt 
R1(config-if)#exit
```
Se decidira al activo a aquel que tenga la mas alta prioridad. 


### Comandos de utilidad 

Para mostrar todas las rutas que conoce nuestro dispositivo: 

```sh
ESW1# sh ip route
```

Para ver el resumen del estado del protocolo HSRP:

```sh
ESW1# sh standby brief
```

Para ver todas las vlans configuradas en nuestro equipo:

```sh
ESW1# sh vlan-switch
```

Para ver la totalidad de la configuracion de nuestro equipo:
```sh
ESW1# sh running-config
```

Para guardar los cambios realizados:
```sh
ESW1# write memory
```


## Estados de los Puertos de la Topologia 2

![image](https://user-images.githubusercontent.com/37676214/99899494-5c82cc80-2c6f-11eb-9877-e3cb377d6e8e.png)


## Ruta principal de STP

![image](https://user-images.githubusercontent.com/37676214/99899525-9e137780-2c6f-11eb-9a64-0ecb4a025d50.png)
