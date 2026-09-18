# Bcho NAM Player 1.7.5 - Manual de usuario (standalone)

Referencia completa de la aplicación standalone para Windows, macOS y Linux.
Aquí está documentado cada control, ventana, archivo y mensaje. Para el plugin
VST3 / AU, consulta el [manual del plugin](PLUGIN_MANUAL.es.md).

---

## Contenido

1. [Qué es Bcho NAM Player](#1-qué-es-bcho-nam-player)
2. [Instalación y primer arranque](#2-instalación-y-primer-arranque)
3. [Mapa de la ventana](#3-mapa-de-la-ventana)
4. [Inicio rápido: sonido en cinco pasos](#4-inicio-rápido-sonido-en-cinco-pasos)
5. [Audio Setup: dispositivo, latencia y ruteo](#5-audio-setup-dispositivo-latencia-y-ruteo)
6. [Recorrido de la señal](#6-recorrido-de-la-señal)
7. [El rack: bloques, orden y el ojo](#7-el-rack-bloques-orden-y-el-ojo)
8. [BLOCK NAM 1 y BLOCK NAM 2](#8-block-nam-1-y-block-nam-2)
9. [Respuestas impulsionales de pantalla](#9-respuestas-impulsionales-de-pantalla)
10. [Los mandos, uno a uno](#10-los-mandos-uno-a-uno)
11. [Los ocho efectos al detalle](#11-los-ocho-efectos-al-detalle)
12. [MONO y STEREO: dos equipos completos](#12-mono-y-stereo-dos-equipos-completos)
13. [Enlazar efectos entre L y R](#13-enlazar-efectos-entre-l-y-r)
14. [Afinador](#14-afinador)
15. [Input Cali (calibración automática de entrada)](#15-input-cali-calibración-automática-de-entrada)
16. [TONE3000 dentro del reproductor](#16-tone3000-dentro-del-reproductor)
17. [Presets portables .bnpp](#17-presets-portables-bnpp)
18. [Qué se recuerda y dónde](#18-qué-se-recuerda-y-dónde)
19. [Ajustes, acabados, actualizaciones y apoyo](#19-ajustes-acabados-actualizaciones-y-apoyo)
20. [Vúmetros y conos animados](#20-vúmetros-y-conos-animados)
21. [Referencia de ratón y teclado](#21-referencia-de-ratón-y-teclado)
22. [Resolución de problemas](#22-resolución-de-problemas)
23. [Especificaciones técnicas](#23-especificaciones-técnicas)
24. [Integridad, código de terceros y licencias](#24-integridad-código-de-terceros-y-licencias)

---

## 1. Qué es Bcho NAM Player

Bcho NAM Player es un procesador de guitarra standalone y portable. Reproduce
capturas Neural Amp Modeler (`.nam`), respuestas impulsionales de pantalla
(`.wav`) y una cadena reordenable de efectos de estudio, y gestiona él mismo el
dispositivo de audio: driver, canales, frecuencia de muestreo, tamaño de búfer y
ruteo a salidas físicas se configuran dentro de la aplicación.

El reproductor tiene **dos rutas de señal completas e independientes**, izquierda
y derecha. Cada ruta tiene su propio BLOCK NAM 1, BLOCK NAM 2, IR de pantalla,
rack de efectos, orden de bloques, puerta de ruido, sección de tonos, volumen
máster, IR blend, volumen de pantalla, ganancias de entrada y salida,
interruptor de encendido, calibración y afinador. En **MONO** solo suena la ruta
izquierda y los controles de la derecha se ocultan; en **STEREO** funcionan las
dos a la vez.

**Qué incluye el paquete**

| Elemento | Notas |
| --- | --- |
| `Bcho NAM Player.exe` (o `.app` / AppImage) | La aplicación completa; sin instalador ni DLL adicionales |
| `Models` | Dos capturas NAM de demostración. **No** se cargan solas |
| `IRs` | Carpeta que abre por defecto el navegador de IR. No se incluye ninguna IR de pantalla |
| `NAM_A2_HEAD.xml` | Aparece tras el primer cierre normal: tu sesión guardada |
| `tone3000.session` | Aparece solo al conectar una cuenta TONE3000 (cifrado) |

> La ventana se abre centrada a su tamaño nativo de 1537 x 1023 siempre que la
> pantalla lo permita. Todo el diseño es adaptable —mueble, mandos, listas,
> vúmetros y textos escalan juntos— y no puede reducirse por debajo del 50 % del
> tamaño nativo, así que ningún control ni rótulo puede salirse de su placa.

---

## 2. Instalación y primer arranque

Descarga el paquete de tu sistema desde la
[última versión pública](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest),
descomprímelo y mantén juntos todos los archivos y carpetas.

| Sistema | Cómo se ejecuta |
| --- | --- |
| Windows x64 | Ejecuta `Bcho NAM Player.exe`. Instala el driver ASIO del fabricante de tu interfaz para la latencia más baja |
| macOS Apple Silicon | Usa el ZIP `arm64` y abre `Bcho NAM Player.app` |
| macOS Intel | Usa el ZIP `x86_64` y abre `Bcho NAM Player.app` |
| Linux x86_64 | Ejecuta el AppImage; usa `chmod +x BchoNAMPlayer-*.AppImage` si no arranca |

Las versiones de macOS tienen firma ad-hoc pero **no** están notarizadas. Si
Gatekeeper bloquea el primer arranque, haz clic derecho en la aplicación y elige
**Abrir**.

**Cómo es el primer arranque.** El reproductor arranca en MONO, con todos los
bloques desactivados, sin modelo ni IR cargados y con el dispositivo de audio
predeterminado del sistema. Una cadena completamente en bypass deja pasar la
señal seca: no enmudece. Lo primero es el
[Audio Setup](#5-audio-setup-dispositivo-latencia-y-ruteo) y después cargar una
captura.

Cada arranque posterior restaura la última sesión que cerraste con normalidad:
controles, las dos rutas, recursos, orden de bloques, efectos y estados de
bypass.

---

## 3. Mapa de la ventana

![El standalone en MONO con una captura, una pantalla y dos efectos activos](manual/img/standalone-mono.jpg)

La ventana tiene tres muebles, de arriba abajo:

**1 - La tira del rack.** Bahía de presets a la izquierda, los bloques de
proceso reordenables en el centro, el botón y la pantalla del afinador, el
selector de afinación y, a la derecha, el conmutador MONO / STEREO y el engranaje
de ajustes.

**2 - La cabeza del amplificador.** Vúmetro de entrada, INPUT GAIN e INPUT CALI a
la izquierda; los siete mandos principales y, encima, los selectores de NAM e
IR; los dos navegadores de archivos (modelos NAM a la izquierda, archivos IR a
la derecha) con el fader IR VOL entre ellos y la columna de salida; vúmetro de
salida, OUTPUT GAIN y el interruptor rojo POWER a la derecha.

**3 - La pantalla acústica.** El logotipo Bcho y dos conos que se mueven con el
nivel real de salida.

![Bahía de presets, conmutador de entrada y primeros bloques del rack](manual/img/zone-preset-bay.jpg)

El rótulo bajo **LOAD PRESET** indica siempre qué están editando los controles
compartidos en ese momento; por ejemplo `PATH R · NAM 2`, o `MONO · NAM 1`.

---

## 4. Inicio rápido: sonido en cinco pasos

1. **Abre Audio Setup.** Pulsa el engranaje (arriba a la derecha del rack) →
   **AUDIO SETUP**. Elige driver e interfaz, marca la entrada donde tienes
   enchufada la guitarra, ajusta frecuencia de muestreo y tamaño de búfer, y
   comprueba que **MAIN / POST MASTER** apunta a las salidas de tus monitores.
2. **Carga una captura de amplificador.** Pulsa **BROWSE LOCAL** bajo NAM MODELS
   y elige un archivo `.nam` o una carpeta entera. La captura se carga, BLOCK
   NAM 2 se ilumina y el archivo aparece en la lista.
3. **Carga una pantalla.** Pulsa **BROWSE IR** y elige una respuesta impulsional
   `.wav`. El bloque IR se ilumina. (Sáltatelo si tu captura ya incluye pantalla:
   muchas capturas «amp_cab» la incluyen.)
4. **Ajusta niveles.** Toca y mira el vúmetro de entrada: busca la zona verde con
   los rasgueos más fuertes rozando el amarillo. Ajusta con INPUT GAIN. Después
   pon MASTER VOL y OUTPUT GAIN a un nivel de escucha cómodo.
5. **Toca.** Añade efectos pulsando sus bloques; doble clic abre su editor.

> Empieza con un nivel de escucha bajo y evita oír la guitarra dos veces: por la
> monitorización directa de la interfaz **y** por el reproductor.

---

## 5. Audio Setup: dispositivo, latencia y ruteo

Engranaje → **AUDIO SETUP**.

![Ventana Audio I/O: ruteo de dispositivo, ruteo de salida y referencia de calibración](manual/img/dialog-audio-setup.png)

**Ruteo de dispositivo (mitad superior)**

| Control | Qué hace |
| --- | --- |
| Audio device type | La familia de driver: ASIO, Windows Audio, DirectSound (Windows); CoreAudio (macOS); ALSA/JACK (Linux). **ASIO da la latencia más baja en Windows** |
| Output | La interfaz que reproduce el sonido procesado |
| Input | La interfaz donde está conectada la guitarra |
| Canales activos | Marca el canal de entrada de la guitarra y el par de salida de tus monitores |
| Sample rate | 44,1 kHz o superior. Más frecuencia cuesta más CPU; las capturas NAM se remuestrean internamente cuando hace falta |
| Audio buffer size | El compromiso entre latencia y estabilidad. 128 o 256 muestras es un buen punto de partida |
| Control panel / Test | Abre el panel del fabricante (ASIO) y reproduce un tono de prueba |

**Ruteo de salida (abajo a la izquierda).** Cuatro tomas independientes, cada una
asignada a un par de salidas físicas o en **Off**:

| Ruta | Señal que lleva | Uso habitual |
| --- | --- | --- |
| MAIN / POST MASTER | La salida final del reproductor | Escucha y grabación del sonido definitivo |
| PRE / NEUTRAL NAM | BLOCK NAM 2 antes de tonos, efectos y pantalla | Reamplificación, comparación A/B |
| DI / CLEAN INPUT | La entrada de la interfaz sin tocar | Pista limpia de seguridad |
| WET / POST CAB | La rama procesada posterior a la pantalla | Ruta de grabación procesada aparte |

Un par solo puede usarlo una ruta: si eliges uno ya ocupado, ese selector vuelve
a **Off**. MAIN usa normalmente las salidas 1/2. Deja en Off las rutas que no
necesites para que nada se duplique.

**Interface input reference / 0 dBFS peak (abajo a la derecha).** Un deslizador
de 0 a 30 dBu. Le dice a [Input Cali](#15-input-cali-calibración-automática-de-entrada)
cuál es el nivel máximo de entrada de tu interfaz. No tiene efecto con Input Cali
desactivado.

Todo lo de esta ventana —dispositivo, canales, frecuencia, búfer, referencia y
las cuatro rutas— se guarda por máquina y se restaura en el siguiente arranque.
Deliberadamente **no** se guarda en los presets `.bnpp`, para que un preset pueda
viajar entre ordenadores.

---

## 6. Recorrido de la señal

Cada ruta procesa su audio en este orden:

```
entrada de la interfaz
  → toma del afinador (siempre la DI sin tocar, antes de todo)
  → INPUT GAIN (+ desplazamiento de Input Cali)
  → GATE
  → [ bloques del rack, en el orden que se ve en pantalla ]
        ...efectos antes de BLOCK NAM 2...
        BLOCK NAM 1  (con sus propios BASS/MID/TREBLE/PRESENCE)
        BLOCK NAM 2  (después, los BASS/MID/TREBLE/PRESENCE principales)
        ...efectos entre BLOCK NAM 2 e IR...
        IR  (convolución de pantalla → IR VOL → IR BLEND)
        ...efectos después de IR...
  → MASTER VOL
  → OUTPUT GAIN
  → POWER
  → rutas de salida MAIN / PRE / DI / WET
```

BLOCK NAM 2 e IR son **anclas**: no se pueden arrastrar, y ningún bloque puede
moverse de forma que IR quede antes de BLOCK NAM 2. Todo lo demás es libre.

---

## 7. El rack: bloques, orden y el ojo

![Las dos filas del rack en STEREO: BLOCK NAM 1 (rojo), BLOCK NAM 2 (dorado), un CHOR activo y los iconos de cadena que enlazan L y R](manual/img/zone-rack-stereo.jpg)

Once bloques por ruta, mostrados de izquierda a derecha en orden de proceso. El
orden por defecto es COMP · OCT · PITCH · BLOCK NAM 1 · BLOCK NAM 2 · CHOR ·
FLANG · PHASE · IR · DELAY · REVERB.

**Cómo se lee un bloque**

![Las partes de un bloque: nombre, ojo, LED, barra de color e icono de enlace](manual/img/zone-block-icons.jpg)

| Parte | Significado |
| --- | --- |
| Color del cuerpo | Iluminado y teñido = activado. Gris plano = en bypass |
| LED pequeño, arriba a la izquierda | Repite el estado de activación |
| Barra de color, abajo | El color identificativo del bloque, encendido mientras está activo |
| Ojo, arriba a la derecha | Elige qué bloque describen los controles compartidos y los navegadores. El bloque visualizado tiene el ojo verde |
| Cadena, abajo a la derecha | Solo en STEREO y solo en efectos: el enlace L/R. Ver el [capítulo 13](#13-enlazar-efectos-entre-l-y-r) |

**Qué hace cada clic**

| Acción | Resultado |
| --- | --- |
| Clic simple en el cuerpo | Activa o pone en bypass el bloque |
| Doble clic en el cuerpo | Efectos: abre el editor. BLOCK NAM 1 / BLOCK NAM 2: abre el selector de modelo. IR: abre el selector de IR |
| Clic en el ojo | Hace que ese bloque sea el que editan los controles compartidos. Un bloque en bypass no se puede visualizar |
| Arrastrar en horizontal | Mueve el bloque; la posición de destino se marca con un contorno blanco |
| Soltar un archivo sobre un bloque | Lo carga: `.nam` en un bloque NAM, `.wav` en el bloque IR; una carpeta carga su primer archivo válido |
| Pasar el ratón por BLOCK NAM 1 / BLOCK NAM 2 | Muestra la ficha de información de la captura |

Un bloque NAM o IR solo se puede activar cuando contiene un archivo válido.
Pulsar uno vacío mientras su archivo aún se carga significa «enciéndelo cuando
esté listo», no «invierte el estado».

---

## 8. BLOCK NAM 1 y BLOCK NAM 2

Los dos bloques admiten cualquier captura `.nam` compatible; el reproductor no
presupone qué se capturó. BLOCK NAM 1 va antes en la cadena y es el sitio natural
para una captura de pedal o previo, y BLOCK NAM 2 para un amplificador, pero nada
impide usarlos al revés.

![Los dos navegadores: modelos NAM a la izquierda con sus cuatro selectores, archivos IR a la derecha, IR VOL entre ambos](manual/img/zone-browsers.jpg)

**Cómo cargar una captura**

| Vía | Cómo |
| --- | --- |
| BROWSE LOCAL | Elige un `.nam` o una carpeta. Una carpeta añade a la lista todas sus capturas y selecciona la primera. Marca **DEEP SEARCH** en el diálogo para incluir subcarpetas |
| La lista | Pulsa cualquier fila para cargarla; los botones ▲ / ▼ recorren la lista y se apagan en los extremos |
| TONE3000 | Abre la biblioteca en línea dentro del reproductor; ver el [capítulo 16](#16-tone3000-dentro-del-reproductor) |
| Arrastrar y soltar | Suelta un `.nam` o una carpeta sobre la lista o directamente sobre el bloque |
| Doble clic en el bloque | Abre el selector de archivos de ese bloque |

Cada bloque recuerda su propia carpeta, su ajuste de búsqueda profunda, su lista
y su selección, por ruta. Elegir una captura para BLOCK NAM 2 devuelve además los
controles de esa ruta a valores seguros y enciende el bloque; la selección de
pantalla no se toca.

**La arquitectura es automática.** El reproductor identifica NAM A1, A2 Standard
y A2 Nano, y despacha los modelos A2 por la vía rápida de NAM Core. No hay
conmutador manual. Si un archivo no es un NAM válido de una entrada y una salida,
la carga se rechaza y el bloque se queda como estaba.

**La ficha de información de la captura.** Al pasar el ratón por un bloque NAM o
por cualquier fila de la lista aparecen los metadatos escritos en la cabecera del
`.nam` —título, marca y modelo del equipo, quién lo modeló, tipo de equipo,
arquitectura, frecuencia de muestreo y nivel de referencia de entrada— además de
la carátula cuando existe.

![La ficha de información de la captura](manual/img/tone-card.png)

La carátula es cualquier imagen que esté junto a la captura con el mismo nombre
base (`Mi Captura.nam` → `Mi Captura.png`, `.jpg`, `.jpeg` o `.webp`). Las
descargas de TONE3000 la guardan solas; para tus propias capturas, basta con
dejar una imagen al lado. Solo se lee la cabecera del archivo, así que recorrer
una lista larga con el ratón no cuesta nada.

**Cargar BLOCK NAM 1 desde el panel frontal.** El botón **+ BLOCK NAM 1** del
rack (y la pestaña NAM 1) pregunta de dónde debe venir la captura:

![Elegir el origen para BLOCK NAM 1](manual/img/dialog-block-nam1.png)

---

## 9. Respuestas impulsionales de pantalla

**BROWSE IR** carga una respuesta `.wav`, o una carpeta: el reproductor se queda
con los archivos WAV cortos que sirven como respuesta impulsional, los lista y
selecciona el primero. Si no encuentra ninguno válido, avisa con **IR not found**.

- Se aceptan respuestas mono y estéreo; un archivo estéreo se suma a mono.
- Se usan hasta 8192 muestras, remuestreadas a la frecuencia del dispositivo.
- **Se conserva la ganancia original: las IR nunca se normalizan.**
- Pulsa otra vez la fila seleccionada para deseleccionarla: se borra la respuesta
  y el bloque IR queda en bypass.
- **DELETE** borra la respuesta seleccionada de la carpeta de IR, tras preguntar.
- Cargar o cambiar una respuesta se hace con fundido cruzado, así que no chasquea.

Dos controles dan forma a la pantalla:

![IR VOL, con su propia escala y el rótulo (L)/(R) en STEREO](manual/img/zone-ir-volume.jpg)

- **IR BLEND** mezcla la señal sin convolución de pantalla con la señal
  convolucionada, de 0 a 100 %.
- **IR VOL** (el fader vertical) ajusta el nivel de la rama de pantalla,
  **de -24 dB a 0 dB**, con **-12 dB** por defecto para dejar margen a las
  capturas con mucho nivel. El valor actual se imprime bajo la escala.

---

## 10. Los mandos, uno a uno

![La fila de mandos principales y los selectores de NAM/IR encima](manual/img/zone-tone-controls.jpg)

**Cómo se usa un mando**: arrastra en vertical u horizontal; el valor exacto se
imprime debajo. **Doble clic restaura el valor por defecto**: las 12 en punto en
todos menos GATE, que vuelve al extremo izquierdo (OFF).

| Control | Rango | Por defecto | Notas |
| --- | --- | --- | --- |
| INPUT GAIN | -12 … +12 dB | 0.0 dB | Nivel hacia la cadena NAM; Input Cali se suma encima |
| GATE | OFF … umbral de -80 a 0 dB | OFF | En el extremo izquierdo es bypass real. Ataque 1,5 ms, retención 35 ms, caída 90 ms, histéresis de 3 dB |
| BASS | ±12 dB @ 70 Hz | 0.0 dB | Campana, Q 0,72 |
| MID | ±12 dB @ 750 Hz | 0.0 dB | Campana, Q 0,72 |
| TREBLE | ±12 dB @ 4 kHz | 0.0 dB | Campana, Q 0,72 |
| PRESENCE | ±12 dB @ 6 kHz | 0.0 dB | Campana, Q 0,72 |
| MASTER VOL | -12 … +12 dB | 0.0 dB | Después de la cadena, antes de Output Gain |
| IR BLEND | 0 … 100 % | 50 % | Seco frente a pantalla |
| IR VOL | -24 … 0 dB | -12 dB | Solo la rama de pantalla |
| OUTPUT GAIN | -12 … +12 dB | 0.0 dB | Nivel final |
| POWER | Encendido / apagado | Encendido | Enmudece la ruta procesada; el interruptor brilla en rojo encendido |
| INPUT CALI | Encendido / apagado | Apagado | Ver el [capítulo 15](#15-input-cali-calibración-automática-de-entrada) |

**La sección de tonos sigue al bloque NAM seleccionado.** Con un selector
**NAM 1** activo, BASS / MID / TREBLE / PRESENCE controlan los cuatro filtros
propios de BLOCK NAM 1; con un selector **NAM 2** activo controlan la sección de
tonos principal. Cada juego guarda sus propios valores y cambiar de selector los
recupera. En STEREO la placa imprime cuál estás editando.

![Columna de entrada: vúmetro, INPUT GAIN e INPUT CALI con su LED](manual/img/zone-input-column.jpg)
![Columna de salida: vúmetro, OUTPUT GAIN y POWER](manual/img/zone-output-column.jpg)

---

## 11. Los ocho efectos al detalle

Cada efecto ofrece **tres algoritmos** y **seis parámetros**. Doble clic en un
bloque abre su editor; cada mando muestra una unidad real y el doble clic sobre
un mando restaura su valor por defecto.

![El editor de efecto, aquí para DELAY](manual/img/dialog-effect-editor.png)

El interruptor **ACTIVE** de la esquina superior derecha del editor es el mismo
bypass que pulsar el bloque. **TYPE** elige el algoritmo. Los cambios de
parámetro, algoritmo y bypass se suavizan, las lecturas de la familia del delay
se interpolan y la realimentación está acotada, así que nada chasquea ni se
dispara.

### COMP - compresor
Algoritmos: **Studio VCA**, **Optical**, **FET Punch**.

| Parámetro | Rango | Por defecto |
| --- | --- | --- |
| Threshold | -55 … -2 dB | -31.2 dB |
| Ratio | 1 … 20 :1 | 7.7:1 |
| Attack | 1 … 100 ms | 15.9 ms |
| Release | 20 … 600 ms | 223 ms |
| Makeup | -12 … +12 dB | 0.0 dB |
| Mix | 0 … 100 % | 100 % |

### DELAY
Algoritmos: **Digital Studio**, **Tape Echo**, **Analog BBD**.

| Parámetro | Rango | Por defecto |
| --- | --- | --- |
| Time | 20 … 1200 ms | 398 ms |
| Feedback | 0 … 92 % | 32 % |
| Mix | 0 … 100 % | 28 % |
| Tone | 0 … 100 % | 65 % |
| Mod | 0 … 100 % | 8 % |
| Level | -12 … +12 dB | 0.0 dB |

### CHOR - chorus
Algoritmos: **Studio**, **Ensemble**, **Tri-Chorus**.

| Parámetro | Rango | Por defecto |
| --- | --- | --- |
| Rate | 0,05 … 5 Hz | 1.24 Hz |
| Depth | 0,5 … 20 ms | 10.3 ms |
| Mix | 0 … 100 % | 35 % |
| Delay | 4 … 30 ms | 11.8 ms |
| Feedback | -65 … +65 % | 0 % |
| Level | -12 … +12 dB | 0.0 dB |

### FLANG - flanger
Algoritmos: **Analog**, **Through-Zero**, **Jet**.

| Parámetro | Rango | Por defecto |
| --- | --- | --- |
| Rate | 0,03 … 2,5 Hz | 0.57 Hz |
| Depth | 0,1 … 9 ms | 5.0 ms |
| Mix | 0 … 100 % | 35 % |
| Feedback | -85 … +85 % | 20 % |
| Manual | 0,2 … 5 ms | 1.4 ms |
| Level | -12 … +12 dB | 0.0 dB |

### PHASE - phaser
Algoritmos: **4 Stage**, **8 Stage**, **12 Stage**.

| Parámetro | Rango | Por defecto |
| --- | --- | --- |
| Rate | 0,03 … 4 Hz | 0.82 Hz |
| Depth | 0 … 100 % | 70 % |
| Mix | 0 … 100 % | 40 % |
| Feedback | -75 … +75 % | 12 % |
| Centre | 180 … 2200 Hz | 887 Hz |
| Level | -12 … +12 dB | 0.0 dB |

### REVERB
Algoritmos: **Studio Room**, **Plate**, **Concert Hall**.

| Parámetro | Rango | Por defecto |
| --- | --- | --- |
| Size | 0 … 100 % | 55 % |
| Damping | 0 … 100 % | 50 % |
| Mix | 0 … 100 % | 25 % |
| Width | 0 … 100 % | 80 % |
| Freeze | OFF / ON | OFF |
| Level | -12 … +12 dB | 0.0 dB |

### OCT - octavador
Algoritmos: **Poly Clean**, **Classic Mono**, **Organ**.

| Parámetro | Rango | Por defecto |
| --- | --- | --- |
| Oct Down | 0 … 100 % | 45 % |
| Oct Up | 0 … 100 % | 0 % |
| Dry | 0 … 100 % | 80 % |
| Tone | 0 … 100 % | 50 % |
| Tracking | 0 … 100 % | 65 % |
| Level | -12 … +12 dB | 0.0 dB |

### PITCH - transpositor
Algoritmos: **Studio**, **Low Latency**, **Vintage**.

| Parámetro | Rango | Por defecto |
| --- | --- | --- |
| Semitones | -12 … +12 st | 0.0 st |
| Mix | 0 … 100 % | 100 % |
| Window | 20 … 120 ms | 65 ms |
| Feedback | 0 … 55 % | 0 % |
| Fine | -100 … +100 ct | 0 ct |
| Level | -12 … +12 dB | 0.0 dB |

---

## 12. MONO y STEREO: dos equipos completos

![STEREO con SPLIT L/R: dos filas de rack, cuatro selectores NAM, dos selectores IR y vúmetros estéreo](manual/img/standalone-split.jpg)

**MONO / STEREO** (arriba a la derecha del rack) alterna entre una y dos rutas
audibles.

![El conmutador MONO / STEREO y el engranaje de ajustes](manual/img/zone-mode-switch.jpg)

- **MONO**: la entrada de la interfaz se suma a la cadena izquierda y su
  resultado alimenta los dos canales de cada par de salida ruteado. Se ocultan
  los selectores de la derecha, la segunda fila del rack y el conmutador de
  entrada.
- **STEREO**: funcionan las dos cadenas. Aparecen dos filas de rack, los vúmetros
  se dividen en L y R, y las pestañas `L` / `R` junto a los racks eligen qué ruta
  editan los controles compartidos.

**DUAL MONO / SPLIT L/R** (junto a la bahía de presets, solo en STEREO):

| Posición | Tratamiento de la entrada |
| --- | --- |
| DUAL MONO | La entrada sumada de la interfaz alimenta **las dos** cadenas: una guitarra por dos equipos independientes |
| SPLIT L/R | El canal de entrada 1 alimenta la cadena izquierda y el canal 2 la derecha |

Este ajuste pertenece al estado de la aplicación, no a los presets.

**Los selectores.**

![NAM 1 L · NAM 2 L · NAM 1 R · NAM 2 R e IR L · IR R](manual/img/zone-selectors.jpg)

| Selector | Elige |
| --- | --- |
| `NAM 1 L` `NAM 2 L` `NAM 1 R` `NAM 2 R` | El bloque NAM sobre el que actúan los controles de tono y el navegador de NAM |
| `IR L` `IR R` | La pantalla sobre la que actúan IR BLEND e IR VOL |
| Pestañas `L` / `R` | La ruta sobre la que actúa cualquier otro control compartido |

**Qué sigue cada control**

| Control | Sigue a |
| --- | --- |
| INPUT GAIN, GATE, MASTER VOL, OUTPUT GAIN, POWER, INPUT CALI, TUNER | la **ruta** seleccionada |
| BASS, MID, TREBLE, PRESENCE | el **bloque NAM** seleccionado de esa ruta (NAM 1 tiene el suyo) |
| IR BLEND, IR VOL | la **pantalla** seleccionada |
| Afinación de referencia, acabado, Audio Setup, ruteo, actualizaciones | toda la aplicación |

En MONO solo se muestran los dos selectores izquierdos, y el rótulo IR VOL pierde
el sufijo `(L)` / `(R)`.

---

## 13. Enlazar efectos entre L y R

En STEREO puedes fijar un efecto de la cadena izquierda al mismo efecto de la
derecha, para ajustarlo una sola vez.

![Los pares enlazados salen en verde; los no enlazados en gris. Un par que ya no comparte columna muestra su icono en la esquina de ambos bloques](manual/img/zone-rack-stereo.jpg)

- **Dónde está el icono.** Cuando los dos bloques están en la misma columna, un
  icono de cadena se sitúa en la junta entre las dos filas del rack y los une. Si
  mueves uno y el par deja de compartir columna, el icono pasa a la **esquina
  inferior derecha de cada bloque**: funciona exactamente igual.
- **Color.** Verde = enlazado. Gris = no enlazado.
- **Clic para enlazar o desenlazar.**
- **Qué se comparte:** el algoritmo y los seis parámetros. Editar cualquiera de
  los dos bloques cambia ambos.
- **Qué no se comparte:** el interruptor de activación y la posición en la
  cadena. Los dos bloques pueden estar activos, ninguno, o uno sí y otro no:
  enlazar nunca los toca.
- **Enlazar dos bloques con ajustes distintos** pregunta qué lado conservar:

![Elegir qué lado se conserva](manual/img/dialog-link-choice.png)

- **Desenlazar** deja los dos bloques exactamente como suenan en ese momento; a
  partir de ahí se editan por separado.
- **BLOCK NAM 1, BLOCK NAM 2 e IR no se pueden enlazar.**
- Los enlaces se guardan con la sesión y dentro de los presets `.bnpp` de dos
  rutas.

---

## 14. Afinador

![La fila del afinador: el botón TUNER, la pantalla de LED y el selector de afinación](manual/img/zone-tuner-row.jpg)

Pulsa **TUNER**; las letras se iluminan en verde y el botón se ve pulsado. La
pantalla muestra la nota detectada con una indicación de LED a izquierda y
derecha para bajo, centrado o alto.

- El afinador escucha la **DI sin tocar**, antes de la puerta, los bloques NAM y
  los efectos, y no forma parte del orden arrastrable.
- Rango aproximado de **65 a 700 Hz**, a cualquier frecuencia de muestreo de 44,1
  a 192 kHz.
- Dentro de **±5 cents** la pantalla indica centrado y se pone verde; más allá de
  unos 40 cents se pone roja.
- **TUNING** ofrece **STANDARD**, **DROP D**, **D STANDARD**, **Eb** y
  **OPEN G**.
- Toca una sola cuerda aislada con buen nivel y deja que la nota anterior se
  apague.

---

## 15. Input Cali (calibración automática de entrada)

Las capturas NAM se entrenan a un nivel de entrada conocido. Input Cali ajusta tu
interfaz a ese nivel para que una captura suene como se capturó.

Con Input Cali activo, el reproductor calcula:

```
ganancia de calibración (dB) = referencia de entrada de la interfaz (dBu) - referencia de entrada del NAM (dBu)
```

- El valor de la interfaz es el deslizador de
  [Audio Setup](#5-audio-setup-dispositivo-latencia-y-ruteo).
- El valor del NAM viene de los metadatos `input_level_dbu` de la captura.
- Si una captura no tiene metadatos, se asume la referencia NAM estándar de
  **+12 dBu**.
- El resultado se limita a **-24 … +24 dB** y se aplica antes de los bloques NAM.
- El LED pequeño junto a INPUT CALI está verde mientras está activo.
- Mientras una captura de sustitución se está cargando, se mantiene la ganancia
  de la captura en curso: nunca salta a 0 dB en mitad de una nota.

Input Cali solo cambia ganancia. Nunca reescribe ni normaliza un modelo. Si tu
interfaz tiene varios modos de entrada (instrumento / línea / atenuador),
introduce el valor en dBu del modo que estés usando realmente. Para una PreSonus
Studio 24c es +10 dBu.

---

## 16. TONE3000 dentro del reproductor

**TONE3000** (botón verde sobre la lista de NAM) abre la biblioteca de capturas
en línea en una ventana del reproductor.

![Antes de conectar una cuenta](manual/img/tone3000-connect.png)

**Conectar una sola vez.** El primer uso pide conectar tu cuenta. TONE3000 inicia
sesión con un enlace por correo, así que eso abre su página de acceso una vez; el
reproductor guarda después el token de refresco devuelto, cifrado con una clave
derivada de esta máquina, en `tone3000.session` junto a la aplicación. Cada
listado y descarga posterior renueva el token en silencio, así que en ese
ordenador no vuelve a hacer falta un navegador. **SIGN OUT** borra el archivo.

![La biblioteca: cinco listas, carátulas, autor, número de modelos y paginación](manual/img/tone3000-library.png)

**Navegar y preescuchar.**

| Elemento | Qué hace |
| --- | --- |
| TRENDING · LATEST · FAVOURITES · DOWNLOADED · MINE | Los cinco listados que puede leer una integración del nivel gratuito |
| Seleccionar una fila | **Carga la captura en el bloque NAM actual al instante.** La primera captura del tone se descarga y suena en cuanto está en disco; el resto del tone y su carátula siguen descargándose en segundo plano |
| Seleccionar otra fila | Cancela lo que quede descargando y preescucha la nueva |
| Un tone que ya habías descargado | Se carga al instante desde tu carpeta de descargas |
| Filas marcadas **IR only - no NAM** | Solo contienen respuestas impulsionales; no hay nada que cargar en un bloque NAM, así que no se preescuchan |
| RESTORE PREVIOUS MODEL | Devuelve la captura que tenía el bloque **antes de abrir esta ventana**. Desactivado si el bloque estaba vacío |
| Cerrar la ventana | Conserva la última captura preescuchada |
| PREV / NEXT | Paginación |
| El indicador giratorio y la línea de estado | Muestran el progreso: *Downloading tone (n / m)* y después *Playing &lt;captura&gt;* |
| SEARCH FULL CATALOGUE | Abre el buscador propio de TONE3000, con búsqueda y audición, dentro del reproductor. Al elegir un tone el buscador se cierra solo y empieza la descarga |
| SIGN OUT | Olvida la cuenta en este ordenador |

Las descargas se guardan en tu carpeta de descargas de TONE3000, una carpeta por
tone, con la carátula junto a cada captura para que la ficha pueda mostrarla.

**WebView2 (solo Windows).** El acceso integrado y el buscador del catálogo usan
Microsoft WebView2, que viene de serie en Windows 11 y con Edge en Windows 10. Si
falta o no está disponible, el reproductor ofrece una descarga oficial de
Microsoft, tu navegador externo o cancelar: **nunca se instala nada
automáticamente** y el paquete no incluye ningún instalador de Microsoft. El
audio y los archivos locales no necesitan WebView2. macOS usa WKWebView y Linux
recurre al navegador del sistema. Los navegadores externo e integrado no
comparten cookies, así que una sesión creada con una versión anterior puede
requerir un acceso dentro del reproductor.

---

## 17. Presets portables `.bnpp`

**SAVE PRESET** escribe un archivo autocontenido con **las dos rutas**:

- la captura de BLOCK NAM 2 de cada ruta;
- la captura de BLOCK NAM 1 de cada ruta, si está cargada;
- la IR seleccionada de cada ruta, si está cargada (hasta seis recursos
  incrustados);
- orden del rack, algoritmos, todos los parámetros de efecto y cada estado de
  bypass;
- todos los mandos, interruptores y ajustes del afinador;
- los enlaces de efectos L/R.

Los recursos incrustados se verifican con SHA-256 al cargarlos, se extraen a la
caché de presets de la aplicación y se restauran. El dispositivo de audio, la
referencia de interfaz y el ruteo físico quedan fuera a propósito, para que un
preset pueda moverse entre ordenadores.

**LOAD PRESET** lo restaura. Un preset escrito por el reproductor de una sola
ruta, o por NAM PLAYER DUAL, se carga en la **ruta seleccionada**. Un preset
escrito aquí sigue abriéndose en el reproductor antiguo de una ruta, porque la
ruta izquierda también se escribe en el formato plano anterior.

> Debe haber una captura cargada en BLOCK NAM 2 para poder guardar un `.bnpp`.

---

## 18. Qué se recuerda y dónde

**El estado de sesión** se escribe al cerrar con normalidad y se restaura en el
siguiente arranque: las dos rutas, todos los controles, las capturas e IR
seleccionadas, el orden de bloques y los bypass, los enlaces, MONO/STEREO, DUAL
MONO/SPLIT, el acabado, el dispositivo de audio, los canales, la frecuencia, el
búfer, la referencia de interfaz y las cuatro rutas de salida.

| Archivo | Dónde | Qué guarda |
| --- | --- | --- |
| `NAM_A2_HEAD.xml` | Junto a la aplicación si esa carpeta permite escritura; si no, en la carpeta de datos del usuario | La sesión |
| `tone3000.session` | La misma carpeta | El token de refresco cifrado de TONE3000 |
| `Presets` / `PresetCache` | La misma carpeta | Los presets que guardas y los recursos extraídos de los que cargas |
| Carpeta de datos del usuario | Windows `%APPDATA%\Bcho\BchoNAMPlayerDual`, macOS `~/Library/Application Support/Bcho/…`, Linux `~/.config/Bcho/…` | Se usa cuando la carpeta de la aplicación es de solo lectura (paquetes macOS, AppImage) |

Los archivos NAM e IR se referencian por ruta de disco, no se copian dentro de la
sesión: mantenlos donde estaban al guardar. Los presets, en cambio, los
incrustan.

---

## 19. Ajustes, acabados, actualizaciones y apoyo

Pulsa el engranaje a la derecha del rack.

![Ajustes de la aplicación](manual/img/dialog-settings.png)

| Control | Qué hace |
| --- | --- |
| FRONT PANEL SKIN | Previsualiza un acabado al instante |
| APPLY SKIN | Hace permanente el acabado previsualizado. Cerrar sin aplicar restaura el anterior |
| AUDIO SETUP | Abre el [Audio Setup](#5-audio-setup-dispositivo-latencia-y-ruteo) |
| CHECK FOR UPDATES | Compara tu versión con la última publicada |
| AUTO-UPDATES: ON / OFF | Si esa comprobación se hace también al arrancar |
| SUPPORT PROJECT ON KO-FI | Abre `ko-fi.com/bchosoft` en tu navegador |
| CLOSE | Cierra la ventana |

**Los once acabados**: Astra / Obsidian · Tribal / Etched Titanium · Skulls /
Bone & Carbon · Hippie / Sunset Paisley · Graffiti / Electric Ink · Purple
Velvet / Amethyst · Stainless Steel / Precision · Ripped Black Denim / Roadworn ·
Blue Denim / Indigo · Spiderwebs / Black Widow · Classic Black / Levant Tolex.
Todos usan la misma geometría, así que ningún control se mueve; solo cambian
materiales, diseño de mandos y contraste de los rótulos. El plugin usa siempre
Astra / Obsidian.

![El aviso de actualización](manual/img/dialog-update.png)

La comprobación de actualizaciones solo informa de la disponibilidad y abre la
página de descarga si se lo pides. Nunca sustituye archivos, modelos ni presets.

---

## 20. Vúmetros y conos animados

**INPUT VU** muestra el nivel entrante y **OUTPUT VU** el nivel final procesado,
de +6 a -60 dB. En STEREO cada vúmetro se divide en una columna L y otra R.

![La pantalla acústica: los dos conos siguen el nivel real de salida](manual/img/zone-cabinet.jpg)

Los dos conos reaccionan al RMS real de la salida final: tocar más fuerte, o
subir MASTER VOL / OUTPUT GAIN, da mayor excursión; el silencio y POWER apagado
los devuelven suavemente al reposo. Solo se mueve la superficie de los conos:
aros, tornillos, rejilla, mueble y logotipo permanecen fijos. La animación va a
60 fotogramas por segundo en el hilo de interfaz y nunca toca, retrasa ni
realimenta el audio.

---

## 21. Referencia de ratón y teclado

| Dónde | Acción | Resultado |
| --- | --- | --- |
| Cualquier mando | Arrastrar arriba/abajo o izquierda/derecha | Cambia el valor |
| Cualquier mando | Doble clic | Restaura el valor por defecto (GATE vuelve a OFF) |
| Bloque del rack | Clic simple | Activa / bypass |
| Bloque del rack | Doble clic | Abre su editor o su selector de archivo |
| Bloque del rack | Arrastrar en horizontal | Reordena (BLOCK NAM 2 e IR son fijos) |
| Bloque del rack | Soltar un archivo o carpeta | Lo carga en ese bloque |
| Icono de ojo | Clic | Visualiza ese bloque con los controles compartidos |
| Icono de cadena | Clic | Enlaza / desenlaza ese efecto entre L y R |
| Lista NAM o IR | Clic en una fila | La carga |
| Lista IR | Clic otra vez en la fila seleccionada | Deselecciona: borra la respuesta y pone el bloque IR en bypass |
| Lista NAM o IR | Soltar un archivo o carpeta | Lo carga |
| ▲ / ▼ | Clic | Entrada anterior / siguiente de la lista |
| Ventana de diálogo | `Esc` | Cerrar |
| Cualquier control | Pasar el ratón | Muestra su ayuda |

---

## 22. Resolución de problemas

| Síntoma | Qué comprobar |
| --- | --- |
| No suena nada | POWER encendido; la ruta MAIN apunta a las salidas que escuchas; el canal de entrada correcto está marcado en Audio Setup; el vúmetro de entrada se mueve al tocar |
| Suena, pero sin amplificador | Hay una captura cargada y BLOCK NAM 2 está encendido; la cadena no está entera en bypass (una cadena en bypass deja pasar el sonido seco) |
| Un bloque NAM no se enciende | Carga una captura válida en ese bloque y espera a que termine; una captura válida lo activa sola |
| El bloque IR sigue en bypass | Carga una respuesta válida y comprueba que no has pulsado dos veces la fila seleccionada (eso la deselecciona) |
| Chasquidos o cortes al tocar | Sube el búfer de audio, usa el driver ASIO del fabricante en Windows y evita búferes muy pequeños con cuatro bloques NAM activos |
| Una carpeta aparece vacía | Debe contener archivos `.nam`, o respuestas `.wav` cortas y válidas, directamente dentro de la carpeta, salvo que marques DEEP SEARCH |
| El nivel no coincide con otro software NAM | Revisa la referencia de interfaz en Audio Setup y si Input Cali está activo |
| Una captura suena demasiado alta o baja | Revisa IR VOL (-12 dB por defecto) e Input Cali antes de tocar INPUT GAIN |
| La sesión no volvió | El reproductor guarda al cerrar con **normalidad**; tras un cierre forzado se restaura la sesión anterior |
| Faltan modelos o IR | Se referencian por ruta de disco. Devuélvelos a su sitio o carga un preset `.bnpp`, que los incrusta |
| La lista de TONE3000 está vacía | Revisa la cuenta, la red y, en Windows, WebView2; o usa el navegador externo |
| macOS rechaza el primer arranque | Clic derecho en la aplicación y elige **Abrir** |
| El AppImage de Linux no arranca | Dale permiso con `chmod +x` y confirma que el sistema tiene una pila de audio x86_64 funcional |

---

## 23. Especificaciones técnicas

| Elemento | Valor |
| --- | --- |
| Rutas de señal | 2 independientes (L / R) |
| Bloques NAM | 2 por ruta (4 en total) |
| IR de pantalla | 1 por ruta |
| Efectos | 8 por ruta, con 3 algoritmos y 6 parámetros cada uno |
| Posiciones del rack | 11 por ruta, reordenables libremente alrededor de las anclas BLOCK NAM 2 e IR |
| Arquitecturas NAM | A1, A2 Standard, A2 Nano, detectadas automáticamente |
| Frecuencias de muestreo | Las que ofrezca el dispositivo, de 44,1 a 192 kHz |
| Tamaño de búfer | El que ofrezca el driver; el motor usa internamente 32 muestras como mínimo y divide los búferes excesivos |
| Longitud de IR | Hasta 8192 muestras, remuestreadas a la frecuencia del dispositivo, nunca normalizadas |
| Rango del afinador | ~65 - 700 Hz, centrado a ±5 cents |
| Rango de Auto Cal | -24 … +24 dB |
| Fundido de arranque | 60 ms desde silencio |
| Fundido al cambiar de NAM | 15 ms de salida, silencio hasta instalar la captura nueva, 20 ms de entrada (coseno elevado) |
| Fundido al cambiar de IR | 12 ms de fundido cruzado |
| Ventana nativa | 1537 x 1023, adaptable, mínimo 50 % |
| Refresco de interfaz | 60 fps, íntegramente fuera del hilo de audio |

---

## 24. Integridad, código de terceros y licencias

Compara los hashes de los ZIP descargados con `SHA256SUMS.txt`. Bcho NAM Player
incluye JUCE y Neural Amp Modeler Core; sus avisos están en
`THIRD_PARTY_NOTICES.md`.

La aplicación no otorga derechos sobre capturas NAM ni respuestas impulsionales
de terceros. Respeta la licencia que acompaña a cada captura o respuesta, incluso
las que descargues por TONE3000 o compartas dentro de un preset `.bnpp`.
