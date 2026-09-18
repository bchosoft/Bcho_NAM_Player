# Bcho NAM Player 1.7.5 - Manual del plugin VST3 / AU

Referencia completa del plugin. Comparte motor, rack, efectos, biblioteca
TONE3000 y presets con la aplicación standalone, así que este manual documenta el
plugin por completo y remite al [manual del standalone](USER_MANUAL.es.md) en los
capítulos idénticos.

---

## Contenido

1. [Qué es el plugin](#1-qué-es-el-plugin)
2. [Instalación](#2-instalación)
3. [Tu primera pista](#3-tu-primera-pista)
4. [Mapa del editor](#4-mapa-del-editor)
5. [MONO, STEREO y la configuración de canales](#5-mono-stereo-y-la-configuración-de-canales)
6. [Cargar capturas y pantallas](#6-cargar-capturas-y-pantallas)
7. [Controles](#7-controles)
8. [El rack y los ocho efectos](#8-el-rack-y-los-ocho-efectos)
9. [Enlazar efectos entre L y R](#9-enlazar-efectos-entre-l-y-r)
10. [Afinador e Input Cali](#10-afinador-e-input-cali)
11. [TONE3000 dentro del plugin](#11-tone3000-dentro-del-plugin)
12. [Proyectos, presets y automatización](#12-proyectos-presets-y-automatización)
13. [Ajustes y apoyo](#13-ajustes-y-apoyo)
14. [Diferencias con el standalone](#14-diferencias-con-el-standalone)
15. [Resolución de problemas](#15-resolución-de-problemas)
16. [Especificaciones técnicas](#16-especificaciones-técnicas)
17. [Integridad y licencias](#17-integridad-y-licencias)

---

## 1. Qué es el plugin

Un plugin de **efecto de audio**, no un instrumento MIDI. Lleva dos rutas de
señal completas e independientes (L y R), cada una con BLOCK NAM 1, BLOCK NAM 2,
IR de pantalla, rack de ocho efectos con orden libre, puerta de ruido, sección de
tonos, volumen máster, IR blend, volumen de pantalla, ganancias de entrada y
salida, encendido, calibración y afinador.

| Formato | Plataformas |
| --- | --- |
| VST3 | Windows x64, macOS Intel y Apple Silicon, Linux x86_64 |
| AU | Solo macOS |

No se incluye AAX. Usa el paquete que coincida con la arquitectura del proceso de
tu DAW.

---

## 2. Instalación

Cierra antes el DAW y copia el **paquete completo**, no solo el binario de su
interior.

| Sistema | Destino |
| --- | --- |
| Windows | `C:\Program Files\Common Files\VST3` (puede pedir permisos de administrador) |
| macOS VST3 | `~/Library/Audio/Plug-Ins/VST3` |
| macOS AU | `~/Library/Audio/Plug-Ins/Components` |
| Linux | `~/.vst3` |

Arranca el DAW y vuelve a escanear los plugins. El efecto aparece como **Bcho NAM
Player**.

Las versiones de macOS tienen firma ad-hoc, no notarización. Si el host lo
bloquea, revisa Privacidad y seguridad y la validación propia del host; no
desactives globalmente las protecciones del sistema.

---

## 3. Tu primera pista

1. Inserta el plugin como **efecto** en una pista de audio mono o estéreo.
2. Selecciona tu entrada de guitarra en el DAW y activa la monitorización. Evita
   monitorizar la misma señal dos veces, por la interfaz y por el DAW.
3. Una instancia nueva arranca en **MONO** con todos los bloques desactivados,
   así que tu señal seca pasa hasta que cargues una captura. POWER puede
   enmudecer la ruta.
4. Carga una captura con **BROWSE LOCAL** o **TONE3000** y después una pantalla
   con **BROWSE IR**.
5. Ajusta niveles con INPUT GAIN, MASTER VOL y OUTPUT GAIN mirando los vúmetros.

> El driver, la frecuencia de muestreo y el tamaño de búfer son cosa del DAW. El
> plugin no tiene ventana de dispositivo de audio.

---

## 4. Mapa del editor

![El editor del plugin en MONO](manual/img/plugin-mono.jpg)

La disposición es la del standalone menos lo que gestiona el host:

- **Tira del rack**: botones de preset, los once bloques reordenables, el
  afinador y su pantalla, el selector de afinación, el conmutador MONO / STEREO y
  el engranaje de ajustes.
- **Cabeza del amplificador**: vúmetro de entrada, INPUT GAIN, INPUT CALI; los
  siete mandos principales con los selectores de NAM e IR encima; los navegadores
  de NAM e IR con el fader IR VOL; vúmetro de salida, OUTPUT GAIN y POWER.
- **Pantalla acústica**: el logotipo y dos conos movidos por el nivel real de
  salida.

El editor es totalmente redimensionable y mantiene sus proporciones de
1537 x 1023.

---

## 5. MONO, STEREO y la configuración de canales

El plugin presenta siempre una **salida estéreo**, incluso en una pista mono,
para que las dos cadenas tengan siempre a dónde ir.

| Modo | Comportamiento |
| --- | --- |
| MONO | Solo funciona la ruta izquierda. Su resultado se copia a las dos salidas del plugin |
| STEREO | La ruta izquierda procesa el canal de entrada 1 y alimenta la salida 1; la derecha procesa el canal 2 y alimenta la salida 2 |

En una **pista mono en STEREO**, las dos cadenas reciben la misma señal de
entrada, así que una guitarra mueve dos equipos independientes. En una **pista
estéreo en STEREO**, los dos canales de entrada se procesan por separado.

![El plugin en STEREO: dos filas de rack, cuatro selectores NAM, dos selectores IR](manual/img/plugin-stereo.jpg)

El conmutador DUAL MONO / SPLIT L/R del standalone no existe aquí: en un DAW eso
lo decides con el ruteo de la propia pista.

Las pestañas `L` / `R` junto a los racks eligen qué ruta editan los controles
compartidos; los selectores `NAM 1 L`, `NAM 2 L`, `NAM 1 R`, `NAM 2 R` e `IR L`,
`IR R` funcionan igual que en el standalone: ver
[Qué sigue cada control](USER_MANUAL.es.md#12-mono-y-stereo-dos-equipos-completos).

---

## 6. Cargar capturas y pantallas

Idéntico al standalone
([capítulo 8](USER_MANUAL.es.md#8-block-nam-1-y-block-nam-2) y
[capítulo 9](USER_MANUAL.es.md#9-respuestas-impulsionales-de-pantalla)):

- Elige el bloque de destino con los selectores de NAM y usa **BROWSE LOCAL**, la
  lista, **TONE3000**, un doble clic en el bloque, o arrastrar y soltar.
- **BROWSE IR** carga una respuesta `.wav`; pulsar otra vez la fila seleccionada
  la borra y deja el bloque IR en bypass.
- Cargar un archivo válido enciende su bloque. La ganancia de las IR nunca se
  normaliza.
- NAM A1, A2 Standard y A2 Nano se detectan automáticamente.
- Pasar el ratón por un bloque NAM o por una fila de la lista muestra la ficha de
  información de la captura.

Las capturas de demostración van en la carpeta `Models` junto al paquete, pero
nunca se cargan solas; localízalas con BROWSE LOCAL.

> El proyecto del DAW guarda **referencias** a tus archivos `.nam` y `.wav`, no
> los archivos. Mantenlos en su sitio, o guarda presets `.bnpp`, que sí los
> incrustan.

---

## 7. Controles

Rangos, valores por defecto y comportamiento son los del standalone: ver
[Los mandos, uno a uno](USER_MANUAL.es.md#10-los-mandos-uno-a-uno).

En resumen: INPUT GAIN y OUTPUT GAIN ±12 dB; GATE desde OFF hasta un umbral de
-80…0 dB; BASS / MID / TREBLE / PRESENCE ±12 dB a 70 Hz, 750 Hz, 4 kHz y 6 kHz
siguiendo al bloque NAM seleccionado; MASTER VOL ±12 dB; IR BLEND 0-100 %;
IR VOL -24…0 dB (por defecto -12 dB) siguiendo a la pantalla seleccionada; POWER
enmudece la ruta. Arrastra un mando para cambiarlo, doble clic para restaurar su
valor por defecto.

---

## 8. El rack y los ocho efectos

Idéntico al standalone
([capítulo 7](USER_MANUAL.es.md#7-el-rack-bloques-orden-y-el-ojo) y
[capítulo 11](USER_MANUAL.es.md#11-los-ocho-efectos-al-detalle)): clic simple
activa o pone en bypass, doble clic abre el editor o el selector de archivo,
arrastrar reordena alrededor de las anclas BLOCK NAM 2 e IR, y el ojo elige qué
bloque describen los controles compartidos.

![El editor de efecto](manual/img/dialog-effect-editor.png)

Compresor, octavador, transpositor, chorus, flanger, phaser, delay y reverb, cada
uno con tres algoritmos y seis parámetros en unidades reales. Las tablas
completas están en el
[manual del standalone](USER_MANUAL.es.md#11-los-ocho-efectos-al-detalle).

---

## 9. Enlazar efectos entre L y R

En STEREO, el icono de cadena enlaza un efecto de L con el mismo efecto de R, de
modo que una edición cambia los dos. Verde = enlazado, gris = no. Cuando los dos
bloques comparten columna, el icono está en la junta entre las filas; cuando no,
pasa a la esquina inferior derecha de ambos bloques.

![Pares enlazados y no enlazados en las dos filas del rack del plugin](manual/img/zone-rack-stereo.jpg)

Los bloques enlazados comparten el algoritmo y los seis parámetros; cada uno
conserva su interruptor de activación y su posición. Enlazar dos bloques con
ajustes distintos pregunta qué lado conservar. BLOCK NAM 1, BLOCK NAM 2 e IR no
se pueden enlazar. **Los enlaces se guardan en el proyecto del DAW.** Descripción
completa: [capítulo 13 del standalone](USER_MANUAL.es.md#13-enlazar-efectos-entre-l-y-r).

---

## 10. Afinador e Input Cali

**TUNER** funciona igual que en el standalone: escucha la DI sin tocar, antes de
la puerta y de los bloques NAM, cubre de unos 65 a 700 Hz, indica centrado dentro
de ±5 cents y ofrece STANDARD, DROP D, D STANDARD, Eb y OPEN G. Toca una sola
cuerda aislada con buen nivel.

**INPUT CALI** usa la referencia del motor y los metadatos `input_level_dbu` de
la captura (asumiendo +12 dBu cuando no los tiene), limitado a ±24 dB. El plugin
**no** muestra el deslizador de referencia de interfaz del standalone, porque la
interfaz es cosa del DAW: para una calibración concreta de hardware, ajusta la
ganancia fuera del plugin o usa el standalone.

---

## 11. TONE3000 dentro del plugin

El botón **TONE3000** abre la misma ventana de biblioteca que el standalone.

![La biblioteca TONE3000](manual/img/tone3000-library.png)

- Conecta la cuenta una vez; el token de refresco cifrado se guarda por usuario,
  así que el plugin no vuelve a necesitar un navegador en ese ordenador.
- TRENDING, LATEST, FAVOURITES, DOWNLOADED y MINE.
- **Seleccionar una fila carga esa captura en el bloque NAM actual al
  instante**; el resto del tone se descarga en segundo plano, y elegir otra fila
  lo cancela. Un tone que ya tengas descargado se carga al instante.
- Las filas marcadas **IR only - no NAM** solo contienen respuestas
  impulsionales y no se preescuchan.
- **RESTORE PREVIOUS MODEL** devuelve lo que tenía el bloque antes de abrir la
  ventana; al cerrarla se queda la última preescucha.
- **SEARCH FULL CATALOGUE** abre el buscador propio de TONE3000 dentro del
  plugin; al elegir un tone, el buscador se cierra solo y empieza la descarga.

En Windows el navegador integrado usa WebView2. Dentro de un DAW, el plugin
guarda sus datos de WebView2 en una carpeta por usuario, así que un host
instalado en Archivos de programa nunca lo bloquea. Si falta WebView2, el plugin
ofrece una descarga oficial de Microsoft o tu navegador externo, y no instala
nada automáticamente. Detalle completo:
[capítulo 16 del standalone](USER_MANUAL.es.md#16-tone3000-dentro-del-reproductor).

---

## 12. Proyectos, presets y automatización

**El proyecto del DAW** guarda todo lo de la instancia: las dos rutas, cada
control, las referencias a archivos, el orden del rack, los algoritmos, los
parámetros, los estados de bypass, los enlaces L/R y MONO/STEREO.

Al reabrir un proyecto, los NAM, NAM de pedal e IR guardados de **las dos** rutas
vuelven a cargarse en el motor con su estado activado/desactivado, sea cual sea
el orden en que el host restaura el estado y prepara el audio, y con el editor
cerrado. La restauración del proyecto, los cambios de captura y la
reinicialización del audio (un cambio de frecuencia de muestreo o de tamaño de
búfer) entran con fundido desde silencio, así que nada chasquea.

**Presets `.bnpp`.** SAVE PRESET escribe un archivo portable para la **ruta
seleccionada**, con su BLOCK NAM 1, BLOCK NAM 2, IR y ajustes incrustados y
verificados con SHA-256; LOAD PRESET sustituye esa ruta. Comparte las dos rutas
como dos presets; usa el proyecto para recuperar la instancia entera. Un preset
de dos rutas del standalone carga su representación de ruta izquierda en la ruta
seleccionada del plugin.

**Automatización.** El host puede automatizar los parámetros publicados, por
ruta:

| Parámetro | Por ruta |
| --- | --- |
| Input Gain, Gate, Bass, Mid, Treble, Presence, Master Vol | `L_` y `R_` |
| NAM 1 Bass, NAM 1 Mid, NAM 1 Treble, NAM 1 Presence | `L_` y `R_` |
| IR Blend, IR Cabinet Volume, Output Gain | `L_` y `R_` |
| Power, Input Cali, Tuner | `L_` y `R_` |
| Stereo (MONO / STEREO) | uno, global |

El orden del rack, los algoritmos y los parámetros de efecto forman parte del
estado guardado, no de la automatización del host. Cargar un archivo es una
carga, no un parámetro continuo.

---

## 13. Ajustes y apoyo

El engranaje abre una ventana breve con la versión y un enlace para apoyar el
proyecto.

![Ajustes del plugin](manual/img/dialog-plugin-settings.png)

---

## 14. Diferencias con el standalone

| El standalone tiene | El plugin |
| --- | --- |
| Audio Setup: driver, interfaz, canales, frecuencia, búfer | Lo gestiona el DAW |
| Ruteo físico MAIN / PRE / DI / WET | Se rutea dentro del DAW |
| Conmutador de entrada DUAL MONO / SPLIT L/R | Lo decide el ruteo de la pista |
| Deslizador de referencia de interfaz para Input Cali | No se expone; calibra fuera o usa el standalone |
| Once acabados seleccionables | Siempre Astra / Obsidian |
| Su propia sesión guardada entre arranques | El estado viene del proyecto del host |
| Comprobación de actualizaciones | No se incluye |

Todo lo demás —motor, rack, efectos, enlaces, afinador, navegadores, TONE3000,
ficha de información, presets `.bnpp`— es el mismo código.

---

## 15. Resolución de problemas

| Síntoma | Qué comprobar |
| --- | --- |
| No aparece tras escanear | Que carpeta, formato y arquitectura coincidan con el host; vuelve a escanear |
| No hay audio | Entrada de la pista, monitorización, POWER y el ruteo del propio DAW |
| Solo suena la señal seca | Que haya una captura cargada y su bloque encendido; una cadena entera en bypass deja pasar el sonido seco |
| Un lado en silencio en STEREO | El DAW debe alimentar de verdad los dos canales; en una pista mono las dos cadenas reciben la misma entrada |
| Faltan archivos tras mover un proyecto | Restaura la ubicación de los `.nam` / `.wav`, o carga tus presets `.bnpp` |
| Cortes de audio | Sube el búfer y reduce la carga de CPU; cuatro bloques NAM en dos rutas exigen bastante |
| Ventana de TONE3000 vacía | Cuenta, red o WebView2 en Windows; o usa el navegador externo |
| macOS lo rechaza en el host | Revisa la validación del host y los permisos del sistema; la firma ad-hoc no es notarización |
| El proceso del DAW seguía vivo tras cerrar un proyecto | Era un interbloqueo al descargar el plugin, corregido en 1.7.5. Finaliza una vez el proceso sobrante desde el Administrador de tareas y actualiza el plugin |

---

## 16. Especificaciones técnicas

| Elemento | Valor |
| --- | --- |
| Tipo de plugin | Efecto de audio (sin MIDI) |
| Configuración de buses | Entrada mono o estéreo, **salida siempre estéreo** |
| Rutas de señal | 2 independientes (L / R) |
| Bloques NAM | 2 por ruta; IR 1 por ruta; 8 efectos por ruta |
| Frecuencias y búferes | Los que dé el host; los búferes excesivos se dividen internamente |
| Arquitecturas NAM | A1, A2 Standard, A2 Nano, automáticas |
| Fundido de arranque / repreparación | 60 ms desde silencio |
| Fundido al cambiar de NAM | 15 ms de salida, silencio hasta instalar la captura nueva, 20 ms de entrada |
| Fundido al cambiar de IR | 12 ms de fundido cruzado |
| Editor | 1537 x 1023 nativo, redimensionable y proporcional |

---

## 17. Integridad y licencias

Comprueba los hashes de los ZIP con `SHA256SUMS.txt` y lee
`THIRD_PARTY_NOTICES.md` (JUCE y Neural Amp Modeler Core). Respeta las licencias
de las capturas y respuestas impulsionales que uses o compartas dentro de
presets. Estos manuales no implican certificación en todos los DAW; cada
combinación de host y sistema merece una comprobación práctica.
