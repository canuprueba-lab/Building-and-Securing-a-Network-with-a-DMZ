
# Informe de configuración de DMZ con Cisco Packet Tracer


### 1. Objetivo del laboratorio

> Explica brevemente qué se buscaba lograr con este laboratorio.

Se configura una DMZ segura usando un router Cisco ISR, aplicando NAT y ACLs para controlar el tráfico entre LAN, DMZ y red externa.
De esta manera se asegura que lo scolaboradores, desde la red interna de la empresa tenga acceso al servidor web de manera rapida y eficiente tenga o no tenga acceso a internet.

---

### 2. Topología implementada



- Cantidad de redes:  3
- Dispositivos usados:  7 (un Router, 3 switchs 2 computadores normales y un servidor web)

En este ejercicio tenemos como infaestructura inicial 3 resdes cableadas controladas por un router cisco conectado a el ISP.

A su vez estas 3 redes estan controladas por swich capa 3 cada una:

- Red DMZ: es una red espcial con el mas alto nivel de seguridad ya que no solo esta expuesta a internet, si no, que resguarda gran parte de la informacion delicada de la empresa.
- Red interna: es la red que se usa para los proceso internos de la empresa, en general sin salida a internet, la utilizan los colaboradores cuya funcion no depende de constante acceso a internet, por tanto tiene un regimen de seguridad menor a la red DMZ.
- Red externa: es una red en la que se ubican los colaboradores cyuas funciones tiene necesidad constante de contacto con internet, por eso tienen su regimen de seguridad y consideracines especiales.
<img width="902" height="465" alt="image" src="https://github.com/user-attachments/assets/14fb0b58-15ab-4a7d-b7bd-128dbdac943e" />



### 3. Plan de direccionamiento IP


| Dispositivo             | IP         | Máscara     | Gateway   |

|-------------------------|------------|----- -------|-----------|
| PC_Internal             |192.168.1.10|255.255.255.0|192.168.1.1|
| Server_DMZ              |192.168.2.10|255.255.255.0|192.168.2.1|
| PC_External             |192.168.3.10|255.255.255.0|192.168.3.1|
| Router_FW Gi0/0 (LAN)   |192.168.1.1 |255.255.255.0|192.168.1.1|
| Router_FW Gi0/1 (DMZ)   |192.168.2.1 |255.255.255.0|192.168.2.1|
| Router_FW Gi0/2 (Ext)   |192.168.3.1 |255.255.255.0|192.168.3.1|


### 4. Configuración aplicada (resumen)

Si configuran las computadoras y el servidor con las direcciones ips entregadas en la tabla anterior.

Luego se activa el servicio de http el el servidor web.

- Interfaces configuradas con las direcciones entregadas en la tabla:
interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
interface GigabitEthernet0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
interface GigabitEthernet0/2
ip address 192.168.3.1 255.255.255.0
no shutdown
exit

- Configuracion de la NAT:
interface GigabitEthernet0/1
ip nat inside
exit
interface GigabitEthernet0/2
ip nat outside
exit
ip nat inside source static 192.168.2.10 192.168.3.1
end

- ACLs:
ip acc ext HTTP_ONLY_DMZ
permit tcp any host 192.168.3.1 eq 80
exit
int g0/2
ip acce HTTP_ONLY_DMZ in
exit
end
w m
conf t
ip acc ext ANY_DMZ_TRAP
deny ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255
permit ip any any
exit
int g0/1
ip acce ANY_DMZ_TRAP in
exit


### 5. Verificaciones realizadas

- ejecucion del comando ping desde el comand promt de la PC_Internal al router: ✅
- ejecucion del comando ping desde el comand promt de el servidor al router: ✅
- ejecucion del comando ping desde el comand promt de la PC_External al router: ✅
- ejecucion el explorador web desde el PC_External al portal web del servidor atravez de la ip de la NAT: ✅
- ejecucion del comando ping desde el comand promt del servidor al PC_Internal verificando el Bloqueo de acceso desde DMZ a LAN: ✅


### 6. Conclusiones y recomendaciones

> ¿Qué aprendiste con este ejercicio? ¿Qué mejorarías?

Aprendí a aplicar NAT y ACLs en un entorno simulado. Recomiendo verificar conectividad básica antes de aplicar reglas de firewall, ya que un error en la IP puede bloquear todo.

