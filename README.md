# Configuracion_Proyecto_Redes
Manual de configuración de la topología 2 del proyecto del curso Redes de computadoras 1 

## Brian Xiloj
## Abner Cardona

# Proyecto Final Redes1

# Manual de configuracion

## Creación de la topología 1 de red en GNS3.
##### Creando nuevo proyecto
1. Abrir GNS3
2.  Ir a File -> New Blank Project
3. Crear nuevo proyecto, ingresar un nombre de proyecto, elegir la ubicacion en donde se guardara el proyecto y luego click en ok  
![image](https://user-images.githubusercontent.com/37677468/99886080-505f2680-2bff-11eb-9bfb-4816d32654ad.png)
***
##### Agregar dispositivos a grid
1. Mostrar todos los dispositivos
![image](https://user-images.githubusercontent.com/37677468/90541893-8a241b00-e140-11ea-999d-0143b795a373.png)
2. Seleccionar tres veces el router C3725 y arrastrarlo hacia el centro de la aplicación GNS3
![image](https://user-images.githubusercontent.com/37677468/90542032-be97d700-e140-11ea-8b83-d443e1cc60c7.png)
3. Arrastrar cuatro ethernet switch al centro de la aplicacion 
![image](https://user-images.githubusercontent.com/37677468/90542449-5dbcce80-e141-11ea-9af5-511b4b3f4ed1.png)
4. Arrastrar cuatro maquinas virtuales (Tiny Linux) al centro de la aplicacion GNS3
![image](https://user-images.githubusercontent.com/37677468/99886617-9ae2a200-2c03-11eb-8640-10596dc52f4f.png)
5. Arrastrar dos ethernet switch al centro de la aplicacion GNS3
![image](https://user-images.githubusercontent.com/37677468/95883580-575d6400-0d38-11eb-9dcd-5892ea80ed35.png)
6. Arrastrar un Cloud al centro de la aplicacion GNS3
![image](https://user-images.githubusercontent.com/37677468/99886641-d41b1200-2c03-11eb-90b7-d09555e27cc9.png)
7. Nos quedaria algo como sigue:
![image](https://user-images.githubusercontent.com/37677468/99886647-e432f180-2c03-11eb-8304-90835ead3700.png)
8. Ordenar los elementos para una disposicion mas estetica
![image](https://user-images.githubusercontent.com/37677468/99886713-41c73e00-2c04-11eb-8346-a9c2543925ee.png)
***
##### Etiquetar dispositivos
1. Click en el siguiente boton para añadir etiquetas a la topología  
![image](https://user-images.githubusercontent.com/37677468/90542902-1125c300-e142-11ea-88c2-fc73ce6bdbf2.png)  
2. Etiquetar cada elemento  
	a. En base a la siguiente tabla       ![image](https://user-images.githubusercontent.com/37677468/99886946-09c0fa80-2c06-11eb-8477-28fe084d1941.png)  
	b. Quedando de la siguiente forma  
	![image](https://user-images.githubusercontent.com/37677468/99888457-940f5b80-2c12-11eb-9b16-428cec0c4538.png)
***
##### Crear conexiones
1. Usar el siguiente boton para añadir conexiones y luego seleccionar dispositivos y puertos a conectar  
![image](https://user-images.githubusercontent.com/37677468/90543444-f43dbf80-e142-11ea-9607-9a9d4973b8ec.png)
2. Conectar el diagrama para obtener una topología como la que sigue
***
##### Plus: Etiquetar los puertos
![image](https://user-images.githubusercontent.com/37677468/99891340-7fd95780-2c2e-11eb-989b-58936de375a9.png)
***
## Configuracion de la topologia 1 de red en GNS3
### Configuracion Capa de Distribución
#### Configuracion Distribucion1
1. Click derecho en DISTRIBUCION1 y seleccionar start para iniciarlo  
![image](https://user-images.githubusercontent.com/37677468/99891531-66390f80-2c30-11eb-824c-2862bcdf7f7d.png)  
2. Doble click en ESW1 y nos saldra una ventana  
![image](https://user-images.githubusercontent.com/37677468/99891536-8799fb80-2c30-11eb-81de-47ee47a170bf.png)  
3. Ejecutamos lo siguiente: - conf t (para configurar el terminal)  
![image](https://user-images.githubusercontent.com/37677468/99891554-c465f280-2c30-11eb-86b1-3d09f7e806f9.png)
***
###### VTP en Distribucion1 como Server
A. -configure terminal (Para entrar a las configuraciones del terminal)  
B. -vtp domain T1GRUPO27 (Ingresamos dominio y password)  
C. -vtp password T1GRUPO27  
D. -vtp version 2 (Habilitamos el vtp)  
E. -vtp mode server (Porque queremos que este dispositivo replique a todos los demas)  
F. -exit  
![image](https://user-images.githubusercontent.com/37677468/99891599-350d0f00-2c31-11eb-98b5-9459f5461cde.png)
***
###### Configurando las interfaces de Distribucion1
A. - conf t (Para configurar el terminal)  
B. - interface range fastEthernet 1/0 - 15 (Para configurar este rango de interfaces)  
C. - speed 100 (Asignamos velocidad 100)  
D. - duplex full (Le colocamos direccion de doble via)  
E. - no shutdown (Levantamos las interfaces)  
F. - switchport mode trunk (Colocamos todas las interfaces en modo trunk)  
G. - exit  
H. - exit  
![image](https://user-images.githubusercontent.com/37677468/99891905-8e2a7200-2c34-11eb-8671-f526e8c3f77a.png)
***
##### Configuro sus VLAN  
###### Configuro la VLAN 37
1. -conf terminal (Para configurar el terminal)
2. -vlan 37 (Para decir que quiero configurar dicha VLAN)
3. -name RED1 (Le coloco este nombre a la VLAN)
4. -exit  

###### Configuro la VLAN 47
1. -conf terminal (Para configurar el terminal)
2. -vlan 47 (Para decir que quiero configurar dicha VLAN)
3. -name RED2 (Le coloco este nombre a la VLAN)
4. -exit  

###### Configuro la VLAN 57
1. -conf terminal (Para configurar el terminal)
2. -vlan 57 (Para decir que quiero configurar dicha VLAN)
3. -name RED3 (Le coloco este nombre a la VLAN)
4. -exit  

###### Configuro la VLAN 67
1. -conf terminal (Para configurar el terminal)
2. -vlan 67 (Para decir que quiero configurar dicha VLAN)
3. -name RED4 (Le coloco este nombre a la VLAN)
4. -exit  
![image](https://user-images.githubusercontent.com/37677468/99894467-84f7d000-2c49-11eb-82b3-dc7e2741910a.png)
***
##### Configuro las interface VLAN y agrego el HSRP (Activo)  
###### Configuro la interface VLAN 37
1. -conf terminal (Para configurar el terminal)
2. -interface vlan37 (Creo la interfaz virtual de vlan37)
3. -ip address 192.168.10.29 255.255.255.0 (Asigno ip a la interfaz)
4. -standby 37 ip 192.168.10.254 (Asigno ip virutal)
5. -standby 37 priority 120 (Entre mas grande la prioridad el sera el activo)
6. -standby 37 preempt (Indica que es el activo)
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99896381-c2faf100-2c55-11eb-8ae0-fb3fd8d904d7.png)  

###### Configuro la interface VLAN 47
1. -conf terminal (Para configurar el terminal)
2. -interface vlan47 (Creo la interfaz virtual de vlan37)
3. -ip address 192.168.20.29 255.255.255.0 (Asigno ip a la interfaz)
4. -standby 47 ip 192.168.20.254 (Asigno ip virutal al HSRP)
5. -standby 47 priority 120 (Entre mas grande la prioridad el sera el activo)
6. -standby 47 preempt (Indica que es el activo)
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99896420-f6d61680-2c55-11eb-8fd2-1df5abf0ed31.png)  

###### Configuro la interface VLAN 57
1. -conf terminal (Para configurar el terminal)
2. -interface vlan57 (Creo la interfaz virtual de vlan37)
3. -ip address 192.168.30.29 255.255.255.0 (Asigno ip a la interfaz)
4. -standby 57 ip 192.168.30.254 (Asigno ip virutal)
5. -standby 57 priority 120 (Entre mas grande la prioridad el sera el activo)
6. -standby 57 preempt (Indica que es el activo)
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99896443-2f75f000-2c56-11eb-9796-50f5bf564dbe.png)  

###### Configuro la interface VLAN 67
1. -conf terminal (Para configurar el terminal)
2. -interface vlan67 (Creo la interfaz virtual de vlan37)
3. -ip address 192.168.40.29 255.255.255.0 (Asigno ip a la interfaz)
4. -standby 67 ip 192.168.40.254 (Asigno ip virutal)
5. -standby 67 priority 120 (Entre mas grande la prioridad el sera el activo)
6. -standby 67 preempt (Indica que es el activo)
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99896456-5fbd8e80-2c56-11eb-8719-1b214a350a9b.png)  

8. -sh standby brief (Para ver la configuracion)  
![image](https://user-images.githubusercontent.com/37677468/99896470-7f54b700-2c56-11eb-82c6-1eb583bfd9d9.png)

##### Configuro Port Channel  
###### Configuro la interface fastEthernet 1/4 - 7
1. -conf t
2. -interface range fastEthernet 1/4 - 7
3. -channel-group 1 mode on
4. -exit
5. -exit  
![image](https://user-images.githubusercontent.com/37677468/99896639-048c9b80-2c58-11eb-9d64-b739c14bec31.png)
###### Compruebo Port Channel  
1. -sh interfaces port channel 1  
2. -sh etherchannel summary  
![image](https://user-images.githubusercontent.com/37677468/99901770-cc4c8380-2c7e-11eb-819b-4bae836330b3.png)  
##### Configuro Interfaz fastEthernet 1/8  
1. -conf t
2. -interface fastEthernet 1/8
3. -no switchport
4. -ip address 37.0.0.1 255.0.0.0
5. -exit  
![image](https://user-images.githubusercontent.com/37677468/99896783-71546580-2c59-11eb-802f-64b5f040d7ce.png)
##### Configuro Interfaz fastEthernet 1/9  
1. -conf t
2. -interface fastEthernet 1/9
3. -no switchport
4. -ip address 47.0.0.1 255.0.0.0
5. -exit  
![image](https://user-images.githubusercontent.com/37677468/99896819-c2fcf000-2c59-11eb-93f6-911051523b0b.png)
***
#### Configuracion Distribucion2
1. Click derecho en DISTRIBUCION2 y seleccionar start para iniciarlo  
![image](https://user-images.githubusercontent.com/37677468/99896890-53d3cb80-2c5a-11eb-83ca-f5511ec2790b.png)  
2. Doble click en Distribucion2 y nos saldra una ventana  
![image](https://user-images.githubusercontent.com/37677468/99896902-71089a00-2c5a-11eb-87f6-6990cc937450.png)  
***
###### VTP en Distribucion2 como Cliente
A. -configure terminal (Para entrar a las configuraciones del terminal)  
B. -vtp domain T1GRUPO27 (Ingresamos dominio y password)  
C. -vtp password T1GRUPO27  
D. -vtp version 2 (Habilitamos el vtp)  
E. -vtp mode client (Porque queremos que este dispositivo obtenga las vlan)  
F. -exit  
![image](https://user-images.githubusercontent.com/37677468/99896949-d9577b80-2c5a-11eb-8e36-a48743cdb263.png)
***
###### Configurando las interfaces de Distribucion2
A. - conf t (Para configurar el terminal)  
B. - interface range fastEthernet 1/0 - 15 (Para configurar este rango de interfaces)  
C. - speed 100 (Asignamos velocidad 100)  
D. - duplex full (Le colocamos direccion de doble via)  
E. - no shutdown (Levantamos las interfaces)  
F. - switchport mode trunk (Colocamos todas las interfaces en modo trunk)  
G. - exit  
H. - exit  
![image](https://user-images.githubusercontent.com/37677468/99896967-00ae4880-2c5b-11eb-9bc2-b4634035eddf.png)
***
##### VLAN debieron replicarse aqui  
1. -sh vlan-switch (Muestra las vlan replicadas)  
![image](https://user-images.githubusercontent.com/37677468/99897029-8500cb80-2c5b-11eb-9fd9-4ea1ab972bd4.png)
***
##### Configuro las interface VLAN y agrego el HSRP (Pasivo)  
###### Configuro la interface VLAN 37
1. -conf terminal (Para configurar el terminal)
2. -interface vlan37 (Creo la interfaz virtual de vlan37)
3. -ip address 192.168.10.30 255.255.255.0 (Asigno ip a la interfaz)
4. -standby 37 ip 192.168.10.254 (Asigno ip virutal)
5. -standby 37 priority 110 (Entre mas grande la prioridad el sera el activo)
6. -exit  
![image](https://user-images.githubusercontent.com/37677468/99897159-ce054f80-2c5c-11eb-9b18-15dbacd3948f.png)  

###### Configuro la interface VLAN 47
1. -conf terminal (Para configurar el terminal)
2. -interface vlan47 (Creo la interfaz virtual de vlan47)
3. -ip address 192.168.20.30 255.255.255.0 (Asigno ip a la interfaz)
4. -standby 47 ip 192.168.20.254 (Asigno ip virutal al HSRP)
5. -standby 47 priority 110 (Entre mas grande la prioridad el sera el activo)
6. -exit  
![image](https://user-images.githubusercontent.com/37677468/99897188-102e9100-2c5d-11eb-8d82-ce275003eea9.png)  

###### Configuro la interface VLAN 57
1. -conf terminal (Para configurar el terminal)
2. -interface vlan57 (Creo la interfaz virtual de vlan57)
3. -ip address 192.168.30.30 255.255.255.0 (Asigno ip a la interfaz)
4. -standby 57 ip 192.168.30.254 (Asigno ip virutal)
5. -standby 57 priority 110 (Entre mas grande la prioridad el sera el activo)
6. -exit  
![image](https://user-images.githubusercontent.com/37677468/99897216-5683f000-2c5d-11eb-9131-3ad49a7c70e8.png)  

###### Configuro la interface VLAN 67
1. -conf terminal (Para configurar el terminal)
2. -interface vlan67 (Creo la interfaz virtual de vlan67)
3. -ip address 192.168.40.30 255.255.255.0 (Asigno ip a la interfaz)
4. -standby 67 ip 192.168.40.254 (Asigno ip virutal)
5. -standby 67 priority 110 (Entre mas grande la prioridad el sera el activo)
6. -exit  
![image](https://user-images.githubusercontent.com/37677468/99897243-8b904280-2c5d-11eb-8363-265196cf3e3c.png)  

7. -sh standby brief (Para ver la configuracion)  
![image](https://user-images.githubusercontent.com/37677468/99897267-af538880-2c5d-11eb-8234-3408e5ce98e4.png)
***
##### Configuro Port Channel  
###### Configuro la interface fastEthernet 1/4 - 7
1. -conf t
2. -interface range fastEthernet 1/4 - 7
3. -channel-group 1 mode on
4. -exit
5. -exit  
![image](https://user-images.githubusercontent.com/37677468/99897299-ecb81600-2c5d-11eb-9d29-92f85c245ce1.png) 
###### Compruebo Port Channel  
1. -sh interfaces port channel 1  
2. -sh etherchannel summary  
![image](https://user-images.githubusercontent.com/37677468/99901803-061d8a00-2c7f-11eb-8651-1c5cfd595e2b.png)  
***
##### Configuro Interfaz fastEthernet 1/8  
1. -conf t
2. -interface fastEthernet 1/8
3. -no switchport
4. -ip address 57.0.0.1 255.0.0.0
5. -exit  
![image](https://user-images.githubusercontent.com/37677468/99897342-402a6400-2c5e-11eb-86d4-4ac1189e9404.png)
***
##### Configuro Interfaz fastEthernet 1/9  
1. -conf t
2. -interface fastEthernet 1/9
3. -no switchport
4. -ip address 67.0.0.1 255.0.0.0
5. -exit  
![image](https://user-images.githubusercontent.com/37677468/99897359-63551380-2c5e-11eb-83ef-bc7a02dee1ea.png)
***
### Configurar SWITCH1
1. Click derecho en SWITCH1 y seleccionar configure  
![image](https://user-images.githubusercontent.com/37677468/99897755-e2981680-2c61-11eb-8cd1-dc66e5468369.png)  
2. Configurarlo de la siguiente manera dejando modo acceso y modo trunk (dot1q) respectivamente  
![image](https://user-images.githubusercontent.com/37677468/99897794-2ee35680-2c62-11eb-8ef9-ca42c54d1761.png)
***
### Configurar SWITCH2
1. Click derecho en SWITCH2 y seleccionar configure  
![image](https://user-images.githubusercontent.com/37677468/99897834-84b7fe80-2c62-11eb-8611-a3bc9297a2a8.png)  
2. Configurarlo de la siguiente manera dejando modo acceso y modo trunk (dot1q) respectivamente  
![image](https://user-images.githubusercontent.com/37677468/99897858-a913db00-2c62-11eb-948b-23952df911dc.png)
***
### Configurar SWITCH3
1. Click derecho en SWITCH3 y seleccionar configure  
![image](https://user-images.githubusercontent.com/37677468/99897884-ee380d00-2c62-11eb-894d-fcce4a9bf1a3.png)  
2. Configurarlo de la siguiente manera dejando modo acceso y modo trunk (dot1q) respectivamente  
![image](https://user-images.githubusercontent.com/37677468/99897878-e1b3b480-2c62-11eb-9eaf-f79b3e7b47af.png)
***
### Configurar SWITCH4
1. Click derecho en SWITCH4 y seleccionar configure  
![image](https://user-images.githubusercontent.com/37677468/99897889-fa23cf00-2c62-11eb-8b36-a2fb2efb76ce.png)  
2. Configurarlo de la siguiente manera dejando modo acceso y modo trunk (dot1q) respectivamente  
![image](https://user-images.githubusercontent.com/37677468/99897908-1d4e7e80-2c63-11eb-9205-16083ccd4f91.png)
***
### Configurar TinyLinuxVM-1
1. Iniciar maquina virtual  
2. Configurarlo de la siguiente manera  
![image](https://user-images.githubusercontent.com/37677468/99897794-2ee35680-2c62-11eb-8ef9-ca42c54d1761.png)
***
### Configurar TinyLinuxVM-1
1. Iniciar maquina virtual  
2. Configurarlo de la siguiente manera  
![image](https://user-images.githubusercontent.com/37677468/99899768-85a45c80-2c71-11eb-91fe-e614f7741b0d.png)
***
### Configurar TinyLinuxVM2-1
1. Iniciar maquina virtual  
2. Configurarlo de la siguiente manera  
![image](https://user-images.githubusercontent.com/37677468/99899850-dfa52200-2c71-11eb-9948-33db323f0730.png)
***
### Configurar TinyLinuxVM3-1
1. Iniciar maquina virtual  
2. Configurarlo de la siguiente manera  
![image](https://user-images.githubusercontent.com/37677468/99900212-f3ea1e80-2c73-11eb-888c-446a20206769.png)
***
### Configurar TinyLinuxVM4-1
1. Iniciar maquina virtual  
2. Configurarlo de la siguiente manera  
![image](https://user-images.githubusercontent.com/37677468/99900245-14b27400-2c74-11eb-82e6-7782e5440eda.png)
***
### Configurar Nucleo1
1. Iniciar Nucleo1  
2. Entrar en Nucleo1
##### Configurar FastEthernet 0/0
1. -conf t
2. -interface fa0/0
3. -ip address 37.0.0.2 255.0.0.0
4. -no shutdown
5. -duplex full
6. -speed 100
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99902395-25b6b180-2c83-11eb-9569-7a1b7d3ec79a.png)
***
##### Configurar FastEthernet 0/1
1. -conf t
2. -interface fa0/1
3. -ip address 57.0.0.2 255.0.0.0
4. -no shutdown
5. -duplex full
6. -speed 100
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99902435-70382e00-2c83-11eb-8e94-5e7734c9c8a6.png)
***
##### Configurar Serial 1/2
1. -conf t
2. -interface serial 1/2
3. -ip address 77.0.0.1 255.0.0.0
4. -no shutdown
5. -exit  
![image](https://user-images.githubusercontent.com/37677468/99902701-61eb1180-2c85-11eb-84fb-de32b1e674f1.png)
***
##### Configurar RIP
1. -conf t
2. -router rip 
3. -version 2
4. -network 37.0.0.0
5. -network 57.0.0.0
6. -network 77.0.0.0
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99903046-6e706980-2c87-11eb-8266-d26ba471316f.png)
***
### Configurar Nucleo2
1. Iniciar Nucleo2  
2. Entrar en Nucleo2
##### Configurar FastEthernet 0/0
1. -conf t
2. -interface fa0/0
3. -ip address 47.0.0.2 255.0.0.0
4. -no shutdown
5. -duplex full
6. -speed 100
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99902547-3a477980-2c84-11eb-8ec1-c2097c6da390.png)

##### Configurar FastEthernet 0/1
1. -conf t
2. -interface fa0/1
3. -ip address 67.0.0.2 255.0.0.0
4. -no shutdown
5. -duplex full
6. -speed 100
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99902583-78449d80-2c84-11eb-96c7-f93f89fca6d1.png)
***
##### Configurar Serial 1/1
1. -conf t
2. -interface serial 1/1
3. -ip address 87.0.0.1 255.0.0.0
4. -no shutdown
5. -exit  
![image](https://user-images.githubusercontent.com/37677468/99903002-25201a00-2c87-11eb-8c2b-107044b11818.png)
***
##### Configurar RIP
1. -conf t
2. -router rip 
3. -version 2
4. -network 67.0.0.0
5. -network 47.0.0.0
6. -network 87.0.0.0
7. -exit  
![image](https://user-images.githubusercontent.com/37677468/99903060-8ea02880-2c87-11eb-8aeb-38799fa7b03f.png)
***
### Configurar R1
1. Iniciar Nucleo1  
2. Entrar en Nucleo1
##### Configurar Serial 1/2
![image](https://user-images.githubusercontent.com/37677468/99903271-06bb1e00-2c89-11eb-954c-e92a3978018b.png)
***
##### Configurar Serial 1/1
![image](https://user-images.githubusercontent.com/37677468/99903345-61ed1080-2c89-11eb-9a06-7677ad3d7853.png)
***
##### Configurar FastEthernet 0/0
![image](https://user-images.githubusercontent.com/37677468/99903414-d031d300-2c89-11eb-91c0-af20edbeba62.png)
***

## Creación de la topología 2 de red en GNS3.
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
#### Topología 1  
Se capturaron paquetes desde linux1 hasta linux3
![image](https://user-images.githubusercontent.com/37677468/99903759-1be57c00-2c8c-11eb-8db1-2e53f5772d59.png)  

#### Topología 2  

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
