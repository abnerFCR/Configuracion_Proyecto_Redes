# Configuracion_Proyecto_Redes
Manual de configuración de la topología 2 del proyecto del curso Redes de computadoras 1 


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
