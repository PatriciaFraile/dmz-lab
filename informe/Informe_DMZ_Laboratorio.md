Informe de configuración de DMZ con Cisco Packet Tracer

1. Objetivo del laboratorio

El objetivo de este laboratorio fue configurar una DMZ segura utilizando un router Cisco ISR, aplicando NAT estático y listas de control de acceso (ACL) para controlar el tráfico entre la red interna (LAN), la zona DMZ y la red externa.

2. Topología implementada

La red está compuesta por tres redes principales:

Cantidad de redes: 3 (LAN, DMZ y Externa).

Dispositivos usados: Router Cisco ISR, PC_Internal, Server_DMZ y PC_External.

Descripción de las zonas:

LAN: Red interna de la organización.

DMZ: Zona intermedia donde se aloja el servidor web.

Red Externa: Simula Internet desde donde se accede al servicio publicado.

3. Plan de direccionamiento IP

Dispositivo	                IP	                       Máscara	          Gateway

PC_Internal   	        192.168.1.10	           255.255.255.0	192.168.1.1
Server_DMZ	            192.168.2.10	           255.255.255.0	192.168.2.1
PC_External	            192.168.3.10               255.255.255.0	192.168.3.1
Router_FW Gi0/0 (LAN)	192.168.1.1	               255.255.255.0	—
Router_FW Gi0/1 (DMZ)	192.168.2.1	               255.255.255.0	—
Router_FW Gi0/2 (Ext)	192.168.3.1	               255.255.255.0	—

4. Configuración aplicada (resumen)

Durante el laboratorio se configuraron las interfaces del router con las direcciones IP correspondientes y se habilitaron.

También se aplicó NAT estático para publicar el servidor web de la DMZ:

ip nat inside source static 192.168.2.10 192.168.3.1

Se configuraron ACL extendidas para permitir únicamente tráfico HTTP desde Internet y bloquear accesos desde la DMZ hacia la LAN:

access-list 101 permit tcp any host 192.168.3.1 eq 80
access-list 110 deny ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255
access-list 110 permit ip any any

Las ACL fueron aplicadas a las interfaces correspondientes en sentido de entrada.

5. Verificaciones realizadas

Se llevaron a cabo distintas pruebas para comprobar el funcionamiento de la red y las políticas de seguridad:

ping desde PC_Internal al router
Acceso web desde PC_External mediante NAT
Acceso web desde PC_Internal al servidor DMZ
Bloqueo de ping desde la DMZ hacia la LAN
Bloqueo de tráfico desde Internet no autorizado

6. Conclusiones y recomendaciones

Con este ejercicio aprendí a implementar una arquitectura básica con DMZ utilizando NAT y listas de control de acceso.
Como mejora, recomiendo comprobar siempre la conectividad básica antes de aplicar reglas de filtrado, ya que una ACL mal ubicada puede bloquear completamente la comunicación entre redes.
Este laboratorio me ayudó a reforzar conceptos importantes de seguridad perimetral y segmentación de redes.