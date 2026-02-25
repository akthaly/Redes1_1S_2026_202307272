# Manual Técnico - Tarea 3: VTP y VLANs

**Estudiante:** Bryan Alejandro Anona Paredes

**Carnet:** 202307272

**Curso:** Laboratorio de Redes de Computadoras 1

## 1. Objetivos
Implementar una red segmentada utilizando VLANs y el protocolo VTP en modos Servidor, Cliente y Transparente.

## 2. Configuración de VTP y VLANs

### Switch0 (VTP Server)
Se configuró como servidor para propagar las VLANs ADMIN, VENTAS y MERCA.
- **Comando:** `vtp mode server`
- **Evidencia:**
![ev01](../Tarea3/img/01.png)
![ev02](../Tarea3/img/02.png)
![ev03](../Tarea3/img/03.png)
![ev04](../Tarea3/img/04.png)

### Switch ADMIN y VENTAS (VTP Client)
Reciben la configuración de VLANs desde Switch0.
- **Comando:** `vtp mode client`
- **Evidencia:**
![ev05](../Tarea3/img/05.png)
![ev06](../Tarea3/img/06.png)


### Switch MERCA (VTP Transparent)
Se configuró manualmente la VLAN 30 ya que no sincroniza con el servidor.
- **Comando:** `vtp mode transparent`

## 3. Pruebas de Conectividad (Ping)

### Ping Exitoso (Misma VLAN)
De PC de Ventas (192.168.20.2) a PC de Ventas (192.168.20.3).
![ev07](../Tarea3/img/07.png)

### Ping Fallido (Distinta VLAN)
De PC de Ventas a PC de Merca.
![ev08](../Tarea3/img/08.png)