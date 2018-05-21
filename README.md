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
Switch(config)#clock timezone **CST -6**
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
The name for the keys will be: Switch.cic.ipn.mx
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
```


