# Generales

Para poder acceder a la terminal puede ingresar por medio del protocolo “SSH” o “Telnet” por medio de una dirección IP o en su defecto por la interface de consola que se ubica en la parte trasera del dispositivo usando un adaptador serial.

![Cisco Catalyst 2960](cisco-2960.png "Cisco Catalyst 2960")

## Teclas de acceso rápido

Al presionar la tecla “tabulador” dentro de la terminal del Switch la instrucción será completada siempre y cuando no exista ambigüedad causada por más de una instrucción similar.

## Ayuda

Para completar la sintaxis de un comando sin recordar todas sus variaciones basta con usar el carácter de interrogación “?” en la parte desconocida de la instrucción para recibir ayuda dentro de la consola.

## Usuario privilegiado

Para poder efectuar configuraciones tendrá que iniciar como usuario privilegiado utilizando la instrucción “enable” y “configure terminal”

```shell
Switch>enable
Switch#configure terminal
```

La diferencia se puede notar por el indicador de terminal

| | |
|---|---|
| Switch> | Usuario sin privilegios de configuración |
| Switch# | Usuario con privilegios de configuración |

# Configuración del reloj

Existen varias alternativas para ajustar el reloj interno del dispositivo a continuación, las mencionaremos.

## Configuración manual

```shell
Switch#clock set 12:49:00 03 May 2017
```

## Configuración de la zona horaria

La zona horaria CST -6 corresponde a la ciudad de México sin considerar el horario de verano. El cual reduce una hora en el periodo comprendido entre el primer domingo de abril y el último domingo de octubre.

```shell
Switch#configure terminal
Switch(config)#clock timezone CST -6
Switch(config)#clock summer-time CDT recurring 1 Sunday April 1:00 last Sunday October 1:00
```

## Configuración de servidor de tiempo

Para poder habilitar esta opción el dispositivo switch debe contar con acceso a internet para lo cual véase el apartado “Configuración de puerta de acceso”

```shell
Switch#configure terminal
Switch(config)#ntp server time-a.nist.gov version 2
Switch(config)#ntp server time-b.nist.gov version 2
Switch(config)#ntp server time-c.nist.gov version 2
```

## Configuración de puerta de acceso

Las direcciones de la puerta de enlace y resolución de nombres pueden cambiar dependiendo de la configuración de su red.

```shell
Switch#configure terminal
Switch(config)#ip default-gateway 192.168.30.14
Switch(config)#ip name-server 148.204.103.2 148.204.198.2 148.201.235.2
```

## Configuración inicial de seguridad

Los valores resaltados en negritas pueden ser variados de acuerdo a las políticas de la organización y la contraseña mostrada en el siguiente ejemplo es solo una muestra.
En resumen, habilita la conexión por el protocolo **ssh**, deshabilitando el protocolo telnet en todas las líneas vty y se asigna una dirección IP (**192.168.30.13**) al interior de la **vlan 30** y deshabilita el acceso por la **vlan 1**.

Genera un certificado de seguridad RSA de 2048 bits, el más seguro de este dispositivo. Y guarda la configuración de manera permanente en la configuración de inicio. Por lo que puede ser reiniciado sin perder la configuración.

```shell
Switch#configure terminal
Switch(config)#ip ssh version 2
Switch(config)#ip ssh authentication-retries 2
Switch(config)#ip domain name state.gov.ca
Switch(config)#crypto key generate rsa
The name for the keys will be: Switch.state.gov.ca
Choose the size of the key modulus in the range of 360 to 2048 for your
General Purpose Keys. Choosing a key modulus greater than 512 may take
a few minutes.

How many bits in the modulus [512]: 2048
% Generating 2048 bit RSA keys, keys will be non-exportable...[OK]

Switch(config)#interface vlan 30
Switch(config-if)#ip address 192.168.30.13 255.255.255.240
Switch(config-if)#username admin priv 15 secret P@ssw0rd1
Switch(config)#aaa new-model
Switch(config)#enable secret P@ssw0rd2
Switch(config)#line vty 0 15
Switch(config-line)#transport input ssh
Switch(config-line)#end

Switch#configure terminal
Switch(config)#interface vlan 1
Switch(config-if)#no ip address
Switch(config-if)#end

Switch#copy running-config startup-config
Destination filename [startup-config]?
Building configuration...
[OK]
Switch#
```

# Virtual Local Area Network

Una Virtual LAN o VLAN es una red virtual separada por etiquetas que se encuentran identificadas por un numero entero que va desde 0 hasta 4094. Regularmente son utilizadas para separar departamentos, áreas o zonas de trabajo.

## Creación de VLAN

A continuación, crearemos tres VLANs una para acceso a internet (Id 10) otra para el área de servidores (Id 20) y otra para las estaciones de trabajo (Id 30).

```shell
Switch>enable
Switch#configure terminal

Switch(config)#vlan 10
Switch(config-vlan)#name Internet
Switch(config-vlan)#end

Switch(config)#vlan 20
Switch(config-vlan)#name Servidores
Switch(config-vlan)#end

Switch(config)#vlan 30
Switch(config-vlan)#name "Estaciones de trabajo"
Switch(config-vlan)#end
```

## Mostrar VLANs

```shell
Switch#show vlan brief
```

```shell
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active
10   Internet                         active    Gi0/1
20   Servidores                       active    Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22
30   Estaciones de trabajo            active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
Switch#
```

```shell
Switch#show vlan
```

```shell
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active
10   Internet                         active    Gi0/1
20   Servidores                       active    Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22
30   Estaciones de trabajo            active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
10   enet  100010     1500  -      -      -        -    -        0      0
20   enet  100020     1500  -      -      -        -    -        0      0
30   enet  100030     1500  -      -      -        -    -        0      0
1002 fddi  101002     1500  -      -      -        -    -        0      0
1003 tr    101003     1500  -      -      -        -    -        0      0
1004 fdnet 101004     1500  -      -      -        ieee -        0      0
1005 trnet 101005     1500  -      -      -        ibm  -        0      0

Remote SPAN VLANs
------------------------------------------------------------------------------


Primary Secondary Type              Ports
------- --------- ----------------- ------------------------------------------
```

```shell
Switch#show vlan id 20
```

```shell
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
20   Servidores                       active    Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Gi0/2

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
20   enet  100020     1500  -      -      -        -    -        0      0

Remote SPAN VLAN
----------------
Disabled

Primary Secondary Type              Ports
------- --------- ----------------- ------------------------------------------
```

Borrar VLANs

```shell
Switch(config)#no vlan 35
```

**Fuente**

https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960/software/release/12-2_55_se/configuration/guide/scg_2960/swvlan.html

# Listas de control de acceso
Las listas de control de acceso están diseñadas para evitar el acceso desde direcciones de red específicas por una o varias interfaces.

## Creación de lista de control de acceso

A continuación, crearemos una lista de control de acceso que impida el acceso desde direcciones de red privadas por una interface Gigabit Ethernet.

```shell
Switch(config)#ip access-list extended BLACK_LIST
Switch(config-ext-nacl)#deny ip 127.0.0.0 0.255.255.255 any
Switch(config-ext-nacl)#deny ip 192.168.0.0 0.0.255.255 any
Switch(config-ext-nacl)#deny ip host 0.0.0.0 any
Switch(config-ext-nacl)#permit ip any any
Switch(config-ext-nacl)#end
Switch#configure terminal
Switch(config)#interface GigabitEthernet 0/1
Switch(config-if)#ip access-group BLACK_LIST in
Switch(config-if)#end
```

## Mostrar listas de control de acceso

```shell
Switch#show access-list
```

```shell
Extended IP access list BLACK_LIST
    10 deny ip 127.0.0.0 0.255.255.255 any
    20 deny ip 192.168.0.0 0.0.255.255 any
    30 deny ip host 0.0.0.0 any
    40 permit ip any any (4796371 matches)
Switch#
```

## Eliminar listas de control de acceso

```shell
Switch(config)#no ip access-list extended BLACK_LIST
```

**Fuente**

https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960/software/release/12-2_55_se/configuration/guide/scg_2960/swacl.html

# Tablas de direccionamiento MAC

Esta tabla relaciona la dirección física de un equipo (MAC) con la dirección lógica (IP) y con el puerto por el cuan tienen acceso.

## Tiempo de actualización

Esta relación puede causar un problema en redes muy grandes debido a la cantidad de cambios. Ya que al apagar o prender un equipo este debe perder la asignación de IP al interior de un switch. Para mitigar este problema podemos ajustar manualmente el tiempo en que se dará de baja una dirección dentro del switch.

```shell
Switch(config)#mac address-table aging-time 120 vlan 10
```

## Definir rutas estáticas

Esta puede resultar una excelente técnica de mitigación contra la usurpación de la puerta de acceso al interior de una red de trabajo.

```shell
Switch#mac address-table static 50e5.4939.a241 vlan 10 interface GigabitEthernet 0/2
Switch#mac address-table static 50e5.4939.a241 vlan 20 interface GigabitEthernet 0/2
Switch#mac address-table static 50e5.4939.a241 vlan 30 interface GigabitEthernet 0/2
```

## Eliminar rutas estáticas

```shell
Switch#no mac address-table static 50e5.4939.a241 vlan 10 interface GigabitEthernet 0/2
```




