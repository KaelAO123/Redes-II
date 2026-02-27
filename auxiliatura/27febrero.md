
# Apuntes Completos de Redes - Guía de Estudio

## Tema 1: Virtualización de Redes - NAT vs. Adaptador Puente

Cuando trabajamos con máquinas virtuales (VirtualBox, VMware), tenemos que elegir cómo se conectan a la red. Las dos opciones principales son:

| Característica                     | **Modo NAT**                                                                   | **Modo Adaptador Puente (Bridge)**                                                                    |
| ---------------------------------- | ------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| **Funcionamiento**                 | El anfitrión crea una red privada y aislada para la VM (ej. `10.0.2.0/24`).    | La VM se conecta **directamente** a la misma red física que el anfitrión.                             |
| **Dirección IP**                   | La VM obtiene una IP de la red privada del anfitrión (ej. `10.0.2.15`).        | La VM obtiene una IP del mismo rango que la red física (ej. `192.168.1.20`).                          |
| **Acceso a Internet**              | Sí, a través de "traducción" (NAT). El anfitrión actúa como intermediario.     | Sí, directamente como un dispositivo más.                                                             |
| **Visibilidad desde la red local** | La VM es **invisible** para otros dispositivos de la red física.               | La VM es **visible** y accesible desde cualquier otro dispositivo de la red física.                   |
| **Comunicación entre VMs**         | Solo entre VMs que usen la misma red NAT.                                      | Entre VMs en modo puente (si están en la misma red física) y con dispositivos físicos.                |
| **Caso de uso típico**             | Cuando la VM solo necesita salir a Internet, pero no ser accedida desde fuera. | Cuando la VM necesita actuar como un servidor o dispositivo más en la red local (ej. pruebas de red). |

> **Importante:** Una VM en **NAT** y una VM en **Adaptador Puente** están en redes diferentes, por lo que **no pueden comunicarse directamente** a menos que el anfitrión haga un enrutamiento especial.

## Tema 2: Direcciones IP (Versión 4) - A Fondo

Una dirección IP es un identificador único y **lógico** para un dispositivo en una red. Son la base de la comunicación en Internet.

### 2.1. Estructura y Representación

- **Tamaño:** 32 bits.
- **Representación:** Se agrupan en 4 bloques de 8 bits llamados **octetos**, escritos en decimal y separados por puntos. **Ejemplo:** `192.168.1.10`.
- **Dualidad de identificadores:**
  - **Dirección MAC:** Identificador **físico** de la tarjeta de red (capa de enlace). Es único e "inquemable" para esa interfaz. Ejemplo: `74:5d:22:77:93:4e`.
  - **Dirección IP:** Identificador **lógico** (capa de red). Puede cambiar según la red a la que te conectes.

### 2.2. IP Pública vs. IP Privada

- **IP Pública:**
  - Es única en todo el mundo.
  - Es **enrutable en Internet**. Cualquier dispositivo en internet puede (en teoría) alcanzarte con esta IP.
  - La asigna tu Proveedor de Servicios de Internet (ISP).
- **IP Privada:**
  - Se utilizan dentro de redes locales (LAN). Se pueden repetir en diferentes redes locales del mundo.
  - **No son enrutables en Internet.** Los routers de los ISP están configurados para descartar paquetes con estas IPs de origen o destino.
  - Para acceder a Internet, un router con **NAT (Network Address Translation)** traduce la IP privada a su IP pública. Es como si muchas casas (IPs privadas) compartieran una única dirección de correo (IP pública) para recibir paquetes.
  - **Rangos de IPs privadas reservadas (RFC 1918):**
    - **Clase A:** `10.0.0.0` a `10.255.255.255` (máscara `/8`)
    - **Clase B:** `172.16.0.0` a `172.31.255.255` (máscara `/12`)
    - **Clase C:** `192.168.0.0` a `192.168.255.255` (máscara `/16`)

### 2.3. Partes de una IP: Red y Host

Toda dirección IP tiene dos partes fundamentales, definidas por la **máscara de red**:

- **Porción de RED:** Identifica la "calle" o la red específica a la que pertenece el dispositivo.
- **Porción de HOST:** Identifica el "número de casa" o el dispositivo concreto dentro de esa red.
- **Máscara de Red:** Es un número de 32 bits que, en binario, tiene "1"s en la porción de red y "0"s en la porción de host. Se puede representar en formato decimal (`255.255.255.0`) o en notación CIDR (`/24`), que indica el número de bits "1" de la máscara.

**Ejemplo Visual:**
Para la IP `192.168.1.34/24`:

- Máscara: `255.255.255.0` (`/24` significa que los primeros 24 bits son de red).
- Porción de RED: `192.168.1`
- Porción de HOST: `.34`

## Tema 3: Subnetting (Creación de Subredes)

El subnetting es la técnica de "tomar prestados" bits de la porción de **HOST** para crear más **subredes** más pequeñas. Esto permite:

- **Optimizar el uso de direcciones IP:** Asignar redes del tamaño justo para cada departamento o necesidad.
- **Mejorar la organización y la seguridad:** Segmentar una red grande en redes más pequeñas y manejables.
- **Reducir el tráfico de broadcast:** Las tormentas de broadcast se limitan a la subred.

### 3.1. Conceptos y Fórmulas Clave

- **Dirección de Red:** La primera dirección de un rango. Todos los bits de host están a `0`. **No se puede asignar a un host.**
- **Dirección de Broadcast:** La última dirección de un rango. Todos los bits de host están a `1`. Se usa para enviar un mensaje a **todos** los hosts de la red. **No se puede asignar a un host.**
- **Rango Utilizable de Hosts:** Todas las direcciones entre la de red y la de broadcast.

**Fórmulas Fundamentales:**

- **Número de subredes:** `2^n` (donde **n** = número de bits prestados a la porción de red).
- **Número de hosts por subred:** `2^m - 2` (donde **m** = número de bits restantes para la porción de host).
  - *Se restan 2: una para la dirección de red y otra para la de broadcast.*
- **Salto o Incremento:** `256 - (valor del octeto de la máscara que está siendo modificado)`. Este es el número que se suma a la dirección de red anterior para obtener la siguiente.

### 3.2. Ejercicio Práctico 1: FLSM (Máscara de Longitud Fija)

**Escenario:** Te asignan la red `192.168.1.0/24` y necesitas crear **4 subredes** del mismo tamaño.

1. **Calcular bits necesarios (n):** Usamos la fórmula `2^n ≥ 4`. `n=2` porque `2^2 = 4`. Necesitamos prestar 2 bits.
2. **Calcular nueva máscara:** La máscara original es `/24`. Sumamos los 2 bits prestados: `/26`. En decimal, `/26` es `255.255.255.192`.
3. **Calcular hosts por subred:** La máscara `/26` deja `32 - 26 = 6 bits` para hosts. `2^6 - 2 = 64 - 2 = 62 hosts` por subred.
4. **Calcular el salto:** El último octeto de la máscara es `192`. `256 - 192 = 64`. El salto es **64**.
5. **Listar las subredes:**

| Subred | Dirección de Red | Primer Host   | Último Host   | Broadcast     | Máscara |
| ------ | ---------------- | ------------- | ------------- | ------------- | ------- |
| 1      | 192.168.1.0      | 192.168.1.1   | 192.168.1.62  | 192.168.1.63  | /26     |
| 2      | 192.168.1.64     | 192.168.1.65  | 192.168.1.126 | 192.168.1.127 | /26     |
| 3      | 192.168.1.128    | 192.168.1.129 | 192.168.1.190 | 192.168.1.191 | /26     |
| 4      | 192.168.1.192    | 192.168.1.193 | 192.168.1.254 | 192.168.1.255 | /26     |

### 3.3. Ejercicio Práctico 2: VLSM (Máscara de Longitud Variable)

El VLSM es más eficiente. Permite crear subredes de diferentes tamaños para ajustarse a necesidades reales. El truco está en **ordenar las subredes de mayor a menor por cantidad de hosts** y empezar a subnetear desde la más grande.

**Escenario:** Parte de la red `192.168.1.0/24` y necesitas:

- Red A: 100 hosts
- Red B: 25 hosts
- Red C: 10 hosts

Paso 1: Ordenar de mayor a menor.

1. Red A: 100 hosts
2. Red B: 25 hosts
3. Red C: 10 hosts

Paso 2: Subnetear para la Red A (100 hosts)

- Buscamos `2^m - 2 ≥ 100`. `2^6 - 2 = 62` hosts (no alcanza). `2^7 - 2 = 126` hosts (sí alcanza). Necesitamos `m = 7 bits` de host.
- Esto nos da una máscara de `/25` (32-7). En decimal: `255.255.255.128`.
- El salto es `256 - 128 = 128`.
- Asignamos la primera subred a la Red A:
  - **Red A:** `192.168.1.0/25` (IPs: `192.168.1.1` a `192.168.1.126`, Broadcast: `192.168.1.127`).
  - **Siguiente red disponible:** `192.168.1.128`.

Paso 3: Subnetear para la Red B (25 hosts) desde la red disponible

- Parte de la red `192.168.1.128` (aún sin máscara definida). Buscamos para 25 hosts.
- `2^5 - 2 = 30` hosts (sí alcanza). Necesitamos `m = 5 bits` de host.
- Esto nos da una máscara de `/27` (32-5). En decimal: `255.255.255.224`.
- El salto es `256 - 224 = 32`.
- Asignamos la primera sub-red de este "bloque" a la Red B:
  - **Red B:** `192.168.1.128/27` (IPs: `192.168.1.129` a `192.168.1.158`, Broadcast: `192.168.1.159`).
  - **Siguiente red disponible:** `192.168.1.160`.

Paso 4: Subnetear para la Red C (10 hosts) desde la red disponible

- Parte de la red `192.168.1.160`. Buscamos para 10 hosts.
- `2^4 - 2 = 14` hosts (sí alcanza). Necesitamos `m = 4 bits` de host.
- Esto nos da una máscara de `/28` (32-4). En decimal: `255.255.255.240`.
- El salto es `256 - 240 = 16`.
- Asignamos la primera sub-red de este "bloque" a la Red C:
  - **Red C:** `192.168.1.160/28` (IPs: `192.168.1.161` a `192.168.1.174`, Broadcast: `192.168.1.175`).
  - **Siguiente red disponible:** `192.168.1.176` (y así sucesivamente).

## Tema 4: Práctica en Linux - Configuración de Red

### 4.1. Comandos Esenciales (La Navaja Suiza)

- `ip a` (o `ip addr show`): Muestra todas las interfaces y sus direcciones IP.
- `ip route show` (o `ip r`): Muestra la tabla de enrutamiento (incluyendo la puerta de enlace por defecto).
- `ping <IP>`: Prueba de conectividad básica.
- `ss -tulpn`: Muestra los puertos abiertos y escuchando en el sistema.
- `sudo dhclient -v <interfaz>`: Forzar a una interfaz a pedir una IP por DHCP.

### 4.2. Configuración Temporal (hasta reinicio)

```bash
# 1. Asignar una IP estática
sudo ip addr add 192.168.20.50/24 dev enp0s31f6

# 2. Activar la interfaz (si está down)
sudo ip link set enp0s31f6 up

# 3. Agregar la puerta de enlace por defecto (gateway)
#    ¡La IP del gateway DEBE estar en la misma red que tu interfaz!
sudo ip route add default via 192.168.20.1

# 4. Eliminar TODAS las IPs de una interfaz (para empezar de cero)
sudo ip addr flush dev enp0s31f6
```

### 4.3. Configuración Permanente (Estática)

En distribuciones Debian/Ubuntu (si no usan Netplan), editamos el archivo de interfaces.

```bash
sudo nano /etc/network/interfaces
```

El contenido del archivo debe ser algo como esto:

```bash
# Interfaz de loopback (siempre debe estar)
auto lo
iface lo inet loopback

# Configuración estática para mi interfaz Ethernet
auto enp0s31f6
iface enp0s31f6 inet static
    address 192.168.1.100          # La IP de la máquina
    netmask 255.255.255.0           # Máscara de red
    gateway 192.168.1.1             # Puerta de enlace (el router)
    dns-nameservers 8.8.8.8 1.1.1.1 # Servidores DNS (Google y Cloudflare)
```

Para guardar y aplicar: `Ctrl+O`, `Enter`, `Ctrl+X`. Luego:

```bash
sudo systemctl restart networking
# O si el comando anterior falla, a veces funciona:
# sudo /etc/init.d/networking restart
```

## Tema 5: La Tabla de Verdad de las Máscaras (El "Número Mágico")

Esta tabla es la clave para subnetear rápido. El **"Número Mágico"** o **salto** es `256 - (valor de la máscara en el octeto)` .

| Máscara CIDR | Máscara Decimal | Bits de Red | Bits de Host | Nº de Hosts (`2^m - 2`) | Nº Mágico (Salto) |
| ------------ | --------------- | ----------- | ------------ | ----------------------- | ----------------- |
| /24          | 255.255.255.0   | 24          | 8            | 254                     | 256               |
| /25          | 255.255.255.128 | 25          | 7            | 126                     | 128               |
| /26          | 255.255.255.192 | 26          | 6            | 62                      | 64                |
| /27          | 255.255.255.224 | 27          | 5            | 30                      | 32                |
| /28          | 255.255.255.240 | 28          | 4            | 14                      | 16                |
| /29          | 255.255.255.248 | 29          | 3            | 6                       | 8                 |
| /30          | 255.255.255.252 | 30          | 2            | 2                       | 4                 |
| /31          | 255.255.255.254 | 31          | 1            | 0 (Punto a punto)       | 2                 |
| /32          | 255.255.255.255 | 32          | 0            | 1 (Una sola IP)         | 1                 |

## Errores Comunes a Evitar (Checklist)

- [ ] **Asignar la IP de red a un host:** La IP con todos los bits de host en 0 es para identificar la red, no para un PC.
- [ ] **Asignar la IP de broadcast a un host:** La IP con todos los bits de host en 1 es para enviar mensajes a todos.
- [ ] **Olvidar la puerta de enlace (gateway):** Sin ella, tu PC no sabe cómo salir de su propia red para llegar a Internet u otras redes.
- [ ] **Gateway en red diferente:** La IP del gateway debe estar en la **misma red** que la IP de tu máquina.
- [ ] **Mezclar máscaras incompatibles:** Dos dispositivos en la misma red física pero con diferentes máscaras pueden no verse.
- [ ] **Poner la misma IP en dos dispositivos (conflicto de IP):** Causa caos en la red.
