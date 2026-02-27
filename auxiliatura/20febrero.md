<!-- # Cableado y enrutados

# Notas

## 20 de febrero

- La nota total de aux es 5 pts
- La nota seria de 2 practicas (son la misma del Gallardo y del Blacutt)
- Si hay ejercicios en clases valdira poco
- Recomiendan ir a la auxiliaturas porque es un poco jodiditoxd
- Hay que ser capos en subnet
- La primera evaluacion siempre suele ser teorico en un papel nos dira preguntas sobre subnetting, pnsl
- Lo que vale mas son los laboratorios
- La nota se puede ir a:
  - Practicas (4)
  - Asistencia (0.5)
  - Laboratorios (0.5)
- La nota se ira a practicas (2)
  - 2 practicas, cada uno a 2,5
  - La practica sera la misma para los dos paralelos
  - La practica debe de ser a mano
  - En caso de packet tracer una captura
- El proyecto depende de muchas cosas
  - GBS3 es un emulador de packe tracer que seguramente usemos
  - La imagen mas recomendable es Debian 11
  - Con el Blacutt las respues no sean ambiguas, no se tiene que fallar muchos en sus laboratorios, se tiene que estar seguro que se esta haciendo bien
  - El Gallardo te calificara de acuerdo a tus preguntas, por ejemplo, que norma estas usando? Cuando se usa el cable directo. Las preguntas son puras teoricas, del ejercicio 

## Estandares TIA/EIA T568A y T568B
- UTP a partir de 50m ya se considera grande y comienza a fallar

Diferencia de la categoria 5e y 6e es lo grueso que es, tiene la ventja de la cat6 la velocidad

Posbilemente en e lexamen solo nos pida la T-568B
- no es megabytes sino megabits cuando se calcula la red
- En las evaluaciones es individual el material

 -->
# CABLEADO ESTRUCTURADO – GUÍA COMPLETA DE ESTUDIO

## 1. ¿Qué es el Cableado Estructurado?

El **cableado estructurado** es un sistema estandarizado y organizado de cables, conectores, racks y dispositivos que proporciona la infraestructura física para transportar todas las señales de telecomunicaciones (voz, datos, video, control) dentro de un edificio o campus.

A diferencia del cableado "improvisado" (ad-hoc), que se instala según la necesidad del momento, el cableado estructurado se planifica y diseña desde el inicio para ser:

- **Universal:** Soporta múltiples servicios y aplicaciones.
- **Organizado:** Facilita la administración y el mantenimiento.
- **Escalable:** Permite crecer y adaptarse a nuevas tecnologías.
- **Confi able:** Sigue estándares internacionales para garantizar rendimiento.

Su objetivo principal es crear una infraestructura de red que sea independiente de los proveedores y aplicaciones, durando múltiples ciclos de vida de los equipos activos (switches, routers).

## 2. Características Principales

- **Infraestructura Única:** Un mismo sistema de cableado transporta datos, voz y vídeo.
- **Centralización:** Puntos de administración central (MDF, IDF) para facilitar cambios y resolución de problemas.
- **Estandarización:** Sigue normas internacionales (TIA/EIA, ISO/IEC), garantizando compatibilidad y rendimiento.
- **Flexibilidad y Crecimiento:** Diseñado para soportar aplicaciones futuras sin necesidad de reinstalar cableado.
- **Rendimiento Garantizado:** Minimiza interferencias, atenuación y otros problemas físicos.

## 3. Los 6 Subsistemas del Cableado Estructurado (Según Norma TIA/EIA-568)

El sistema se divide en seis subsistemas funcionales, cada uno con una función específica.

### 3.1. Entrada del Edificio (Entrance Facilities)

Es el punto de demarcación física donde el servicio del proveedor externo (ISP) ingresa al edificio.

- **Qué incluye:** Cables de la compañía telefónica, fibra óptica, cables de antena, protecciones contra sobretensiones y el punto de demarcación (el límite entre la responsabilidad del proveedor y la del cliente).
- **Función:** Sirve como interfaz entre la red externa y la red interna del edificio.

### 3.2. Sala de Equipos (Equipment Room)

Es el espacio central y controlado donde reside el equipo de telecomunicaciones más complejo.

- **Qué incluye:** Servidores, switches/core routers, PBX (centralita telefónica), sistemas de respaldo de energía (UPS), y el Distribuidor Principal (MDF).
- **Condiciones especiales:** Debe tener control de temperatura y humedad, pisos técnicos, sistemas de seguridad y extinción de incendios, y energía eléctrica regulada.
- **Diferencia clave:** A diferencia de un Armario de Telecomunicaciones, la Sala de Equipos aloja equipo más complejo y sirve a todo el edificio o a una gran parte de él.

### 3.3. Cableado Troncal (Backbone Cabling)

Es la "columna vertebral" de la red. Proporciona la interconexión entre la Sala de Equipos, los Armarios de Telecomunicaciones y las Entradas del Edificio.

- **Topología:** Generalmente en estrella o jerárquica.
- **Medios de transmisión:**
  - **Fibra Óptica:** Preferida para largas distancias, altas velocidades e inmunidad a interferencias electromagnéticas.
  - **Cobre (UTP/STP):** Para distancias cortas o como respaldo.
- **Función:** Transporta el tráfico consolidado de todas las áreas hacia el equipo central.

### 3.4. Armario de Telecomunicaciones (Telecommunications Room)

Son cuartos o gabinetes distribuidos por el edificio (generalmente uno por piso o área) que conectan el cableado troncal con el cableado horizontal.

- **Qué incluye:** Patch panels, switches de acceso, organizadores de cable, y el Distribuidor Intermedio (IDF).
- **Importancia:** Es el punto de administración donde se realizan la mayoría de las conexiones, cambios y movimientos.

### 3.5. Cableado Horizontal (Horizontal Cabling)

Es el sistema de cables que va desde el Armario de Telecomunicaciones hasta las tomas de usuario en el Área de Trabajo.

- **Topología:** Estrella. Cada toma de usuario tiene un cable dedicado que va al Armario de Telecomunicaciones.
- **Longitud Máxima:** **100 metros** en total, compuestos por:
  - **90 metros** de cable horizontal permanente (desde el patch panel hasta la toma de usuario).
  - **10 metros** sumando los patch cords (cables de conexión) en ambos extremos (en el armario y en el área de trabajo).
- **Medios más comunes:** Cable UTP (Categoría 5e, 6, 6A, 8) o Fibra Óptica.

### 3.6. Área de Trabajo (Work Area)

Es el espacio donde el usuario final se conecta a la red.

- **Qué incluye:** Tomas/conectores de red (jack RJ45) en la pared o en el piso, patch cords (cables de usuario), y los dispositivos finales como computadoras, teléfonos IP, impresoras de red, etc.
- **Nota:** Los dispositivos finales (PCs, impresoras) no forman parte del cableado estructurado en sí, sino que son los elementos que se *conectan a él*.

## 4. Distribuidores Principal y Secundario (MDF/IDF)

- **MDF (Main Distribution Frame / Distribuidor Principal):**
  - Es el punto central de interconexión de toda la red. Se encuentra en la Sala de Equipos.
  - Aquí convergen todos los cables del backbone que vienen de los IDFs y la entrada del edificio.
  - Alberga el equipamiento activo principal (core switches, routers) que gestiona el tráfico de toda la organización.

- **IDF (Intermediate Distribution Frame / Distribuidor Intermedio):**
  - Son puntos de distribución secundarios, ubicados en los Armarios de Telecomunicaciones.
  - Conectan el cableado horizontal de un área o piso específico con el backbone que va hacia el MDF.
  - Albergan switches de acceso y patch panels para esa área.

## 5. Normativas y Estándares Internacionales

El cumplimiento de estándares es lo que define al cableado como "estructurado". Las normas más importantes son:

| Norma             | Ámbito                  | Descripción                                                                                             |
| :---------------- | :---------------------- | :------------------------------------------------------------------------------------------------------ |
| **TIA/EIA-568**   | EE. UU. / Latinoamérica | La más utilizada. Define tipos de cable, distancias, conectores, topología y requisitos de rendimiento. |
| **ISO/IEC 11801** | Internacional           | Estándar global para cableado genérico en edificios comerciales.                                        |
| **EN 50173**      | Europa                  | Normativa europea, muy similar a la ISO/IEC 11801.                                                      |
| **TIA/EIA-569**   | EE. UU.                 | Define espacios y rutas para telecomunicaciones (canalizaciones, cuartos, etc.).                        |
| **TIA/EIA-606**   | EE. UU.                 | Estándar para la administración del cableado (etiquetado, registros).                                   |
| **TIA/EIA-607**   | EE. UU.                 | Especificaciones para sistemas de puesta a tierra (aterrizaje) y protección.                            |

## 6. Tipos de Cable y Categorías

### 6.1. Cable de Par Trenzado (Twisted Pair)

Es el medio más común en redes locales. El trenzado de los pares reduce la interferencia electromagnética y la diafonía (crosstalk) entre pares.

- **UTP (Unshielded Twisted Pair - Par Trenzado Sin Blindar):** El más utilizado por su bajo costo y facilidad de instalación.
- **F/UTP (Blindaje Global):** Tiene una lámina metálica que envuelve todos los pares.
- **STP (Shielded Twisted Pair - Par Trenzado Blindado):** Cada par individual tiene su propio blindaje.
- **S/FTP (Blindaje Global e Individual):** La máxima protección. Cada par va blindado y además hay un blindaje global.

### 6.2. Categorías del Cable UTP (TIA/EIA-568)

| Categoría  | Ancho de Banda | Velocidad Máxima Típica      | Uso Común                                                                  |
| :--------- | :------------- | :--------------------------- | :------------------------------------------------------------------------- |
| **Cat 5e** | 100 MHz        | 1 Gbps (Gigabit Ethernet)    | Redes domésticas y pequeñas oficinas (obsoleto para nuevas instalaciones). |
| **Cat 6**  | 250 MHz        | 1 Gbps / 10 Gbps (hasta 55m) | Redes empresariales estándar. El más común hoy en día.                     |
| **Cat 6A** | 500 MHz        | 10 Gbps (hasta 100m)         | Redes de alto rendimiento, data centers, preparación para el futuro.       |
| **Cat 7**  | 600 MHz        | 10 Gbps                      | Requiere conectores especiales (GG45). No es un estándar TIA. Poco común.  |
| **Cat 8**  | 2000 MHz       | 25/40 Gbps                   | Exclusivo para data centers y distancias muy cortas (hasta 30m).           |

**Nota clave:** La velocidad real depende de toda la cadena: cable, conectores, switch y tarjeta de red del dispositivo.

### 6.3. Fibra Óptica

Utiliza pulsos de luz para transmitir datos. Es inmune a interferencias electromagnéticas y alcanza distancias mucho mayores.

- **Multimodo (MM):** Para distancias cortas y medias (hasta 2 km). Usa LED como fuente de luz. Diámetros comunes: 62.5/125 µm (OM1) y 50/125 µm (OM2, OM3, OM4, OM5).
- **Monomodo (SM):** Para largas distancias (decenas de km). Usa láser como fuente de luz. Diámetro: 9/125 µm (OS1, OS2).

## 7. Conectores y Estándares de Cableado

### 7.1. Conector RJ45

Es el conector físico estándar (8 pines - 8 contactos) para terminar cables de par trenzado en redes Ethernet.

### 7.2. Código de Colores UTP

Los 4 pares trenzados tienen un código de colores estándar:

1. **Par 1:** Blanco-Azul / Azul
2. **Par 2:** Blanco-Naranja / Naranja
3. **Par 3:** Blanco-Verde / Verde
4. **Par 4:** Blanco-Marrón / Marrón

### 7.3. Normas de Ponchado T568A y T568B

Definen el orden de los cables dentro del conector RJ45. Son las dos únicas formas correctas de hacerlo. **Elegir una y mantenerla consistentemente en toda la instalación es fundamental.**

| Pin  | T568A          | T568B              |
| :--- | :------------- | :----------------- |
| 1    | Blanco-Verde   | **Blanco-Naranja** |
| 2    | Verde          | **Naranja**        |
| 3    | Blanco-Naranja | Blanco-Verde       |
| 4    | Azul           | Azul               |
| 5    | Blanco-Azul    | Blanco-Azul        |
| 6    | Naranja        | Verde              |
| 7    | Blanco-Marrón  | Blanco-Marrón      |
| 8    | Marrón         | Marrón             |

### 7.4. Tipos de Cable según la Conexión

- **Cable Directo (Straight-through):** Misma norma en ambos extremos (568B en ambos o 568A en ambos). Es el tipo de cable más común.
  - **Uso:** Conectar dispositivos diferentes (PC a Switch, Switch a Router).
- **Cable Cruzado (Crossover):** Una norma en un extremo (568A) y la otra en el otro (568B).
  - **Uso (Histórico):** Conectar dispositivos iguales (PC a PC, Switch a Switch).
  - **Hoy en día:** Con la tecnología **Auto-MDI/MDIX** (detección automática), los switches y tarjetas de red modernos pueden usar cualquier cable para cualquier conexión, haciendo el cable cruzado prácticamente obsoleto.

## 8. Conceptos Técnicos Clave (Para el Examen)

- **Crosstalk (Diafonía):** Interferencia no deseada de un par de cables sobre otro par cercano.
- **Atenuación:** Pérdida de potencia de la señal a medida que viaja por el cable. Aumenta con la distancia y la frecuencia.
- **AWG (American Wire Gauge):** Sistema para medir el grosor del conductor. Un número más bajo indica un cable más grueso (ej. 22 AWG es más grueso que 24 AWG).
- **Backbone (Troncal):** Cableado vertical que interconecta diferentes pisos o armarios.
- **Patch Panel (Panel de Parcheo):** Panel donde terminan los cables horizontales, permitiendo conexiones flexibles y ordenadas con switches mediante patch cords.
- **Patch Cord (Latiguillo):** Cable de conexión corto, flexible, con conectores en ambos extremos.
- **MDF/IDF:** Distribuidor Principal (en sala de equipos) y Distribuidor Intermedio (en armarios de piso).
- **Auto-MDIX:** Función de los switches modernos que detecta automáticamente el tipo de cable y ajusta la conexión, eliminando la necesidad de cables cruzados.

## 9. Buenas Prácticas y Errores Comunes en Instalación

### Buenas Prácticas

- **Respetar la distancia máxima:** No exceder los 100 metros para cable horizontal de cobre.
- **Evitar dobleces pronunciados:** El radio de curvatura mínimo no debe ser inferior a 4 veces el diámetro del cable.
- **Separar de fuentes de interferencia:** Mantener el cableado de red alejado de cables de alimentación eléctrica, motores y luces fluorescentes.
- **Etiquetar absolutamente todo:** Cada cable, cada toma, cada panel debe tener una identificación única y clara (según norma TIA/EIA-606).
- **Usar organizadores:** Para mantener el orden en los racks y facilitar el mantenimiento.
- **Probar la instalación:** Usar un certificador o verificador de cableado para asegurar que cumple la categoría deseada.

### Errores Comunes (Especialmente en Laboratorio)

- **Pelar demasiado el cable:** Dejar mucho cable sin trenzar aumenta la diafonía.
- **No crimpar bien:** Asegurar que los pines del conector hagan buen contacto con los cables.
- **No respetar el orden de colores:** Mezclar los pares es el error más frecuente.
- **No probar el cable con un tester:** Nunca asumir que el cable funciona sin verificarlo.
- **Mezclar 568A y 568B accidentalmente:** Crear un cable cruzado sin querer.
- **No asentar el cable:** Al ponchar, los cables deben llegar hasta el fondo del conector RJ45.
