# Manual Técnico - Práctica 1: Diseño e Implementación de Red LAN

**Universidad de San Carlos de Guatemala**

**Facultad de Ingeniería**

**Escuela de Ciencias y Sistemas**

**Redes de Computadoras 1**

| Nombre | Carnet |
| :--- | :--- |
| **Alejandro Anona** | **202307272** |

---

## 1. Introducción
Este manual presenta el diseño, configuración e implementación de la red LAN para el nuevo edificio corporativo de **Constructiva S.A.** La infraestructura ha sido simulada utilizando **Cisco Packet Tracer**, garantizando la conectividad entre los tres niveles del edificio y sus respectivos departamentos.

Se ha aplicado el estándar de cableado **TIA/EIA-568B** y un esquema de direccionamiento IP estático basado en la red **192.178.72.0/24**, cumpliendo con los requisitos de segmentación, seguridad básica en capa 2 y organización jerárquica solicitada.

## 2. Objetivos
* **General:** Diseñar e implementar una topología de red LAN funcional que interconecte los tres niveles operativos de la empresa, asegurando comunicación total y organizada.
* **Específicos:**
    * Configurar switches Cisco 2960 mediante CLI asegurando el acceso con credenciales personales (`202307272`).
    * Establecer un esquema de direccionamiento IP sin conflictos en la subred `192.178.72.0/24`.
    * Verificar la conectividad total mediante pruebas de Ping y análisis de paquetes ICMP/ARP en modo simulación.

---

## 3. Topología de Red
La red se diseñó siguiendo una estructura jerárquica dividida por los tres niveles físicos del edificio.

### 3.1 Distribución Física
A continuación se describe la organización de los equipos por nivel:

* **Nivel 1 (Recepción y Administración):**
    * Switch Principal: `SW_L1`
    * Departamentos: Recepción (`Recep`), Contabilidad (`Conta`), Legal (`Legal`), Sala de Reuniones (`Reuniones`).
* **Nivel 2 (Diseño y Urbanismo):**
    * Switch Principal: `SW_L2`
    * Departamentos: Arquitectura (`Arqui`), Urbanismo (`Urba`), Sala de Revisión de Planos (`Planos`).
* **Nivel 3 (Ingeniería y Dirección):**
    * Switch Principal: `SW_L3`
    * Departamentos: Dirección General (`Direccion`), Ingeniería Civil (`Ingenieria`), Servidores Principales (`Servidores`).

### 3.2 Diagrama Lógico
![1](/Imagenes/01.png)
![2](/Imagenes/02.png)

---

## 4. Tabla de Direccionamiento IP
Se utilizó la red base **192.178.72.0/24**, donde "72" corresponde a los dos últimos dígitos del carnet.

| Dispositivo / Depto | Hostname | Dirección IP | Máscara |
| :--- | :--- | :--- | :--- |
| **Piso 1** | | | |
| Servidor Recepción | Server_Recep | 192.178.72.10 | 255.255.255.0 |
| PC Recepción (Ejemplo) | PC_Recep_1 | 192.178.72.20 | 255.255.255.0 |
| PC Contabilidad (Ejemplo)| PC_Conta_1 | 192.178.72.30 | 255.255.255.0 |
| PC Legal (Ejemplo) | PC_Legal_1 | 192.178.72.40 | 255.255.255.0 |
| PC Reuniones (Ejemplo) | PC_Reun_1 | 192.178.72.45 | 255.255.255.0 |
| **Piso 2** | | | | |
| Servidor Urbanismo | Server_Urba | 192.178.72.11 | 255.255.255.0 |
| PC Arquitectura (Ejemplo)| PC_Arqui_1 | 192.178.72.50 | 255.255.255.0 |
| PC Urbanismo (Ejemplo) | PC_Urba_1 | 192.178.72.59 | 255.255.255.0 |
| PC Planos (Ejemplo) | PC_Planos_1 | 192.178.72.64 | 255.255.255.0 |
| **Piso 3** | | | | |
| Servidor Ingeniería | Server_Ing | 192.178.72.12 | 255.255.255.0 |
| PC Dirección (Ejemplo) | PC_Dir_1 | 192.178.72.68 | 255.255.255.0 |
| PC Ingeniería (Ejemplo) | PC_Ing_1 | 192.178.72.72 | 255.255.255.0 |
| **Servidores Centrales** | | | | |
| Servidor Principal 1 | Server_Main1 | 192.178.72.13 | 255.255.255.0 |
| Servidor Principal 2 | Server_Main2 | 192.178.72.14 | 255.255.255.0 |
| Servidor Principal 3 | Server_Main3 | 192.178.72.15 | 255.255.255.0 |

---

## 5. Configuración de Switches y VPCs
Todos los switches fueron configurados mediante CLI. Se aseguró el modo privilegiado y el acceso por consola utilizando el número de carnet **202307272** como contraseña.

### 5.1 Comandos Aplicados
El siguiente script se ejecutó en cada switch, variando únicamente el parámetro `hostname`:

```bash
enable
configure terminal
hostname [NOMBRE_DEL_SWITCH]
! Contraseña encriptada de modo privilegiado (Carnet)
enable secret 202307272
! Configuración de línea de consola
line console 0
password 202307272
login
exit
exit
! Guardar configuración
write
```

### 5.2 Evidencia de Configuración de Switches

1. Switch Nivel 1 (Recepción):
![SW-Recepcion](/Imagenes/03.png)

2. Switch Nivel 2 (Arquitectura):
![SW-Arqui](/Imagenes/04.png)

3. Switch Nivel 3 (Dirección General):
![SW-Direccion](/Imagenes/05.png)

### 5.3 Evidencia de configuración de VPCs 

1. PC Recepción:
![ev01](/Imagenes/ev01.png)

2. Laptop Recepción:
![ev02](/Imagenes/ev02.png)

3. PC Contabilidad:
![ev03](/Imagenes/ev03.png)

4. Laptop Contabilidad:
![ev04](/Imagenes/ev04.png)

5. Laptop Legal:
![ev05](/Imagenes/ev05.png)

6. PC Reuniones: 
![ev06](/Imagenes/ev06.png)

7. PC Arquitectura:
![ev07](/Imagenes/ev07.png)

8. Server Urbanismo:
![ev08](/Imagenes/ev08.png)

9. Laptop Ingeniería Civil:
![ev09](/Imagenes/ev09.png)

10. Servidor de Servidores principales
![ev10](/Imagenes/ev10.png)

## 6. Pruebas de Conectividad (Pings)
Se realizaron pruebas de conectividad (Ping) entre diferentes departamentos para verificar que la red es totalmente convergente y que todos los pisos se comunican entre sí.

Evidencia de Pings (10 Pruebas)

1. Recepción -> Contabilidad

![Ping-1](/Imagenes/ping01.png)

2. Legal -> Servidor Principal

![Ping-2](/Imagenes/ping02.png)

3. Arquitectura -> Ingeniería

![Ping-3](/Imagenes/ping03.png)

4. Urbanismo -> Dirección

![Ping-4](/Imagenes/ping04.png)

5. Planos -> Servidor Recepción

![Ping-5](/Imagenes/ping05.png)

6. Ingeniería -> PC Recepción

![Ping-6](/Imagenes/ping06.png)

7. Servidor Principal -> Laptop Dirección

![Ping-7](/Imagenes/ping07.png)

8. Reuniones -> Contabilidad

![Ping-8](/Imagenes/ping08.png)

9. PC Recepción -> PC Arquitectura

![Ping-9](/Imagenes/ping09.png)

10. PC Legal -> PC Urbanismo

![Ping-10](/Imagenes/ping10.png)

## 7. Análisis de Tráfico (Modo Simulación)
Se utilizó el modo simulación de Packet Tracer para analizar el intercambio de paquetes en la red.

### 7.1 Protocolo ARP
Se capturó el paquete ARP (Address Resolution Protocol) utilizado para descubrir la dirección MAC asociada a una IP de destino antes de enviar datos.

![ARP](/Imagenes/ICMP02.png)

### 7.2 Protocolo ICMP
Se verificó el flujo de mensajes Echo Request y Echo Reply (ICMP) durante las pruebas de conectividad exitosas.

![ICMP](/Imagenes/ICMP01.png)

## 8. Conclusiones

Cumplimiento de Diseño: La implementación de una topología jerárquica con 3 switches principales y sub-switches por departamento permitió organizar eficientemente los 10 departamentos solicitados.

Seguridad y Acceso: La configuración de contraseñas (202307272) en la CLI restringe el acceso no autorizado a la configuración física de los equipos.

Escalabilidad: El direccionamiento IP 192.178.72.0/24 fue distribuido dejando márgenes libres entre departamentos, lo que permite agregar nuevos hosts en el futuro sin reconfigurar la red completa.