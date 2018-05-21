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
Switch(config)#clock timezone <strong>CST -6</strong>
Switch(config)#clock summer-time CDT recurring 1 Sunday April 1:00 last Sunday October 1:00
```

## Configuración de servidor de tiempo

Para poder habilitar esta opción el dispositivo switch debe contar con acceso a internet para lo cual véase el apartado “Configuración de puerta de acceso”

```shell
Switch#configure terminal
Switch(config)#ntp server <strong>time-a.nist.gov</strong> version 2
Switch(config)#ntp server <strong>time-b.nist.gov</strong> version 2
Switch(config)#ntp server <strong>time-c.nist.gov</strong> version 2
```


