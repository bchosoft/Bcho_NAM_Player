# Bcho NAM Player 1.8.0 - Manual del plugin VST3 / AU

Referencia del plugin 1.8.0: instalación, rutas, NORMAL / PLUS, archivos NAM/IR,
controles, parámetros de efectos, HARMONIZER, presets y automatización. Los
apéndices incluyen las tablas completas. El reproductor DI exclusivo del
standalone no forma parte del plugin.

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
18. [Apéndice A: referencia completa de efectos](#apéndice-a-referencia-completa-de-efectos)

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

**PAN** (la barra entre las dos filas del rack y el afinador, solo en STEREO):
un fader horizontal que reparte el nivel entre las dos rutas.

| Posición | Resultado |
| --- | --- |
| Centro (`CENTER`, muesca central, marca verde) | L y R suenan a su nivel completo, igual que sin PAN |
| Hacia `L` | La ruta derecha se atenúa progresivamente; en el tope izquierdo (`L 100 %`) solo suena L |
| Hacia `R` | La ruta izquierda se atenúa progresivamente; en el tope derecho (`R 100 %`) solo suena R |

Las letras `L` y `R` de los extremos son testigos: la del lado que se atenúa se
va apagando, y el carril se ilumina desde el centro hacia el lado favorecido.
Ningún lado sube nunca por encima de su nivel en el centro. Doble clic devuelve
el fader al centro; la rueda del ratón lo mueve en pasos finos.

En el plugin PAN es un parámetro automatizable (`Pan`) y se guarda con el proyecto.

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

**Cómo se usa un mando**: arrastra en vertical u horizontal; el valor exacto se
imprime debajo. **Doble clic restaura el valor por defecto**: las 12 en punto en
todos menos GATE, que vuelve al extremo izquierdo (OFF).

| Control | Rango | Por defecto | Notas |
| --- | --- | --- | --- |
| INPUT GAIN | -12 … +12 dB | 0.0 dB | Nivel hacia la cadena NAM; Input Cali se suma al nivel de entrada |
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
| INPUT CALI | Encendido / apagado | Apagado | Ver el Input Cali en el capítulo 10 |

**La sección de tonos sigue al bloque NAM seleccionado.** Con un selector
**NAM 1** activo, BASS / MID / TREBLE / PRESENCE controlan los cuatro filtros
propios de BLOCK NAM 1; con un selector **NAM 2** activo controlan la sección de
tonos principal. Cada juego guarda sus propios valores y cambiar de selector los
recupera. En STEREO la placa imprime cuál estás editando.

---

## 8. El rack y los ocho efectos

Idéntico al standalone
([capítulo 7](USER_MANUAL.es.md#7-el-rack-bloques-orden-y-el-ojo) y
[capítulo 11](USER_MANUAL.es.md#11-los-ocho-efectos-al-detalle)): clic simple
activa o pone en bypass, doble clic abre el editor o el selector de archivo,
arrastrar reordena alrededor de las anclas BLOCK NAM 2 e IR, y el ojo elige qué
bloque describen los controles compartidos.

![El editor de efecto](manual/img/plugin-dialog-effect-editor.png)

Compresor, octavador, transpositor, chorus, flanger, phaser, delay y reverb, cada
uno con tres algoritmos y seis parámetros principales en unidades reales.
El apéndice A incluye las tablas completas y los controles adicionales de HARMONIZER.

### NORMAL / PLUS: cadenas NAM e IR

El interruptor de palanca del extremo izquierdo del rack elige entre dos formas
de usar las capturas NAM:

| Posición | Qué muestra el rack |
| --- | --- |
| NORMAL (palanca abajo) | BLOCK NAM 1 y BLOCK NAM 2, tal como se describe arriba |
| PLUS (palanca arriba) | Un único bloque **NAM / IR** grande, del doble de ancho, en el lugar de BLOCK NAM 1 dentro de la cadena |

![PLUS: un bloque NAM / IR doble por ruta, con la topología de su cadena bajo el nombre](manual/img/zone-plugin-rack-plus.png)

El bloque NAM / IR de PLUS ejecuta una **cadena** de bloques NAM e IR de pantalla. Se enciende y apaga
con un clic y tiene el ojo como cualquier otro bloque NAM; la línea bajo su nombre
resume la cadena, por ejemplo `SERIES 2` o `PARALLEL 2 | 1`. **Haz doble clic** sobre
él para abrir la ventana PLUS CHAIN:

![La ventana PLUS CHAIN en paralelo: ruta A arriba, ruta B abajo, los botones + y la mezcla A / B](manual/img/plugin-dialog-nam-chain.png)

| Elemento | Uso |
| --- | --- |
| Conmutador de línea simple / líneas paralelas | **SERIES**: una sola ruta de IN a OUT. **PARALLEL**: dos rutas, A arriba y B abajo, alimentadas con la misma entrada y mezcladas de nuevo |
| NAM 1A / 2A e IR 1A / 2A (igual en B) | Máximo dos NAM y dos IR por línea. Cada línea conserva un bloque NAM. El audio sigue el orden mostrado |
| Clic en un bloque | Encender / apagar (un bloque vacío abre el menú de carga en su lugar) |
| Doble clic o clic derecho | NAM: cargar captura local o desde TONE3000. IR: cargar WAV, AIFF o FLAC local. Remove block aparece cuando se permite quitar el bloque |
| Soltar un archivo | `.nam` sobre una tarjeta NAM o + NAM; WAV, AIFF o FLAC sobre una tarjeta IR o + IR |
| Ojo (solo tarjetas NAM) | Elegir el bloque NAM que editan BASS, MID, TREBLE y PRESENCE y en el que carga la lista NAM MODELS o TONE3000 |
| `-` (esquina superior derecha) | Eliminar el bloque, previa confirmación. El último NAM de cada línea no se puede quitar; todos los IR se pueden quitar |
| **+ NAM / + IR** | Añadir el tipo elegido; cada botón se desactiva al alcanzar dos bloques de ese tipo. Los nuevos NAM se insertan antes de los IR |
| Nivel del IR | De -24 a +12 dB, inicialmente 0 dB; doble clic para restablecer. WAV, AIFF y FLAC mono o estéreo promediado a mono; hasta 8192 muestras de origen, remuestreadas sin normalización |
| Arrastrar un bloque | Cambiarlo de posición, también a la otra ruta (si respeta los límites de dos NAM y dos IR) |
| MIX A - B (solo PARALLEL) | Mezcla lineal: centro al 50% de cada línea; extremos al 100% de A o B. A diferencia de PAN, el centro no conserva ambas líneas a nivel completo |

Cada bloque NAM de la cadena tiene su propia captura, su interruptor y sus controles
de tono, igual que BLOCK NAM 1 y BLOCK NAM 2. En PLUS los selectores NAM sobre la
placa de tono y sobre la lista pasan a ser uno por ruta, con el nombre del bloque
que se edita (`NAM 2A`), y la lista muestra los modelos NAM de ese bloque.

La primera vez que se activa PLUS, las capturas NORMAL cargadas se copian a la línea A en orden de rack, con sus ajustes de bypass y tono. Si no hay capturas, queda un bloque NAM vacío. El IR general no se copia a las líneas. NORMAL y PLUS guardan ajustes separados: al volver a
NORMAL, BLOCK NAM 1 y BLOCK NAM 2 están exactamente como estaban. El interruptor,
las cadenas y sus capturas se guardan con la sesión, en los presets (el paquete
`.bnpp` incluye todas las capturas e IR de la cadena) y, en el plugin, con el proyecto
del DAW. Todo cambio de la cadena se aplica tras un breve fundido, sin clics. Con
INPUT CALI activado, PLUS calibra según el primer NAM activo de la línea A; la reproducción DI del standalone anula esa calibración de interfaz.

Los IR de una línea se procesan en serie. Para mezclar dos pantallas, coloca una en cada línea paralela y usa A/B MIX. El IR del rack sigue siendo un bloque compartido independiente: ponlo en bypass si utilizas pantallas por línea para evitar filtrar dos veces. Los IR se cargan en segundo plano y guardan nivel, orden y bypass con la cadena. Las cadenas antiguas con más de dos NAM por línea restauran los dos primeros y muestran un aviso; conserva el preset original si necesitas recuperar la configuración anterior.

El bloque PITCH incluye un **HARMONIZER** que sigue la escala (terceras y quintas según la tonalidad, octavas, detección AUTO de tonalidad): ver [HARMONIZER](USER_MANUAL.es.md#harmonizer-armonía-según-la-escala).

---

## 9. Enlazar efectos entre L y R

En STEREO, el icono de cadena enlaza un efecto de L con el mismo efecto de R, de
modo que una edición cambia los dos. Verde = enlazado, gris = no. Cuando los dos
bloques comparten columna, el icono está en la junta entre las filas; cuando no,
pasa a la esquina inferior derecha de ambos bloques.

![Pares enlazados y no enlazados en las dos filas del rack del plugin](manual/img/zone-plugin-rack-stereo.jpg)

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

![La biblioteca TONE3000](manual/img/plugin-tone3000-library.png)

- Conecta la cuenta una vez; el token de refresco cifrado se guarda por usuario,
  para reutilizarlo mientras la autorización sea válida. Si caduca o se revoca, conecta de nuevo.
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
seleccionada**, con sus archivos NAM/IR de NORMAL y PLUS y sus ajustes incrustados y
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
| Pan (solo actúa en STEREO) | uno, global |

El orden del rack, los algoritmos y los parámetros de efecto forman parte del
estado guardado, no de la automatización del host. Cargar un archivo es una
carga, no un parámetro continuo. PLUS guarda modo, topología, archivos, tono, niveles y bypass en el estado, sin añadir parámetros de automatización al host. La reproducción DI no añade controles, parámetros ni estado al plugin.

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
| Reproductor IN / DI, CONFIG DI, transporte y estado de archivos DI | No se incluyen. Reproduce y dirige las pistas DI en el DAW |

Todo lo demás -motor, rack, efectos, enlaces, afinador, navegadores, TONE3000,
ficha de información, presets `.bnpp`- es el mismo código.

---

## 15. Resolución de problemas

| Síntoma | Qué comprobar |
| --- | --- |
| No aparece tras escanear | Que carpeta, formato y arquitectura coincidan con el host; vuelve a escanear |
| No hay audio | Entrada de la pista, monitorización, POWER y el ruteo del propio DAW |
| Solo suena la señal seca | Que haya una captura cargada y su bloque encendido; una cadena entera en bypass deja pasar el sonido seco |
| Un lado en silencio en STEREO | El DAW debe alimentar de verdad los dos canales; en una pista mono las dos cadenas reciben la misma entrada |
| Faltan archivos tras mover un proyecto | Restaura la ubicación de los `.nam` / `.wav`, o carga tus presets `.bnpp` |
| Cortes de audio | Sube el búfer y reduce la carga de CPU; PLUS puede ejecutar ocho NAM entre ambas rutas, además de IR y efectos |
| Ventana de TONE3000 vacía | Cuenta, red o WebView2 en Windows; o usa el navegador externo |
| macOS lo rechaza en el host | Revisa la validación del host y los permisos del sistema; la firma ad-hoc no es notarización |

---

## 16. Especificaciones técnicas

| Elemento | Valor |
| --- | --- |
| Tipo de plugin | Efecto de audio (sin MIDI) |
| Configuración de buses | Entrada mono o estéreo, **salida siempre estéreo** |
| Rutas de señal | 2 independientes (L / R) |
| NORMAL | 2 NAM y 1 IR general por ruta; 8 efectos por ruta |
| PLUS | 2 NAM + 2 IR por línea, hasta 2 líneas por ruta; el IR general sigue separado |
| Versión interna | 1.8.0 (valor numérico 0x10800); VST3 y AU derivan sus metadatos de la misma versión del proyecto |
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

---

## Apéndice A. Referencia completa de efectos

Cada efecto ofrece **tres algoritmos** y **seis parámetros**. Doble clic en un
bloque abre su editor; cada mando muestra una unidad real y el doble clic sobre
un mando restaura su valor por defecto.

![El editor de efecto, aquí para DELAY](manual/img/plugin-dialog-effect-editor.png)

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


#### HARMONIZER (armonía según la escala)

![La ventana de PITCH con la franja HARMONIZER: interruptor, INTERVAL, KEY, SCALE, TUNING y el visor](manual/img/plugin-dialog-harmonizer.png)

La franja inferior de la ventana de PITCH convierte el bloque en un armonizador
inteligente. Con **HARMONIZER** activado, cada nota que tocas recibe una segunda
voz a un intervalo de la escala, de modo que la armonía siempre está en tono:

| INTERVAL | Segunda voz |
| --- | --- |
| OCTAVE UP / OCTAVE DOWN | Siempre una octava; no necesita tonalidad, suena desde la primera nota y funciona también con acordes |
| THIRD UP / THIRD DOWN | La tercera de la escala: **mayor o menor según la nota**. En Do mayor, Do recibe Mi (tercera mayor) y Re recibe Fa (tercera menor); en Do menor, Do recibe Mib |
| FIFTH UP / FIFTH DOWN | La quinta de la escala: justa, o disminuida sobre el séptimo grado (Si -> Fa en Do mayor) |

**KEY y SCALE.** Con KEY en **AUTO** la tonalidad se aprende de las notas que tocas:

- Trabaja sobre las siete notas en uso, que es lo que decide la armonía. Una
  tonalidad se distingue de su homónima (Do mayor / Do menor) por las notas que
  realmente suenan (Mi o Mib, La o Lab, Si o Sib); una tonalidad, su relativa y sus
  modos (Do mayor, La menor, Re dórico...) comparten notas y por tanto armonía.
- La tónica y el modo se nombran según dónde se detiene lo que tocas y, sobre
  todo, dónde reposan las frases: el visor puede indicar `A MINOR`, `D DORIAN`,
  `G MIXOLYDIAN`... Tocar en pentatónica se interpreta como menor / mayor natural
  hasta que otras notas digan lo contrario. La **menor armónica** se reconoce cuando
  la séptima elevada se usa de forma constante (Sol# y nunca Sol en La menor): la
  dominante recibe entonces su tercera mayor.
- Trabajan dos memorias a la vez: una larga mantiene estable la tonalidad y una
  corta sigue un cambio real de tonalidad en pocos segundos. Una nota de paso
  nunca cambia la tonalidad.
- Hasta haber oído suficientes notas el visor muestra **LISTENING...** y las
  terceras y quintas no suenan, así que nunca se añade una nota equivocada. La
  barra bajo la tonalidad indica lo segura que es la detección.

Elige una tónica en **KEY** para fijar tú la tonalidad; **SCALE** ofrece entonces
mayor, menor, los otros cinco modos, menor armónica y menor melódica.

**TUNING.** **PURE** afina cada intervalo respecto a la nota tocada con proporciones
simples (terceras 5:4 y 6:5, quintas 3:2): las dos voces encajan sin batidos, que es
lo que mantiene limpia una armonía a través de un ampli saturado. **TEMPERED** usa
los semitonos iguales del piano, para coincidir exactamente con teclados.

**La voz.** La armonía la genera un desplazador propio cuyos empalmes se
sincronizan con el periodo de la nota que suena, de modo que suena a segunda
guitarra y no a efecto. Lee la guitarra con unos milisegundos de retraso -el
retraso natural de un segundo músico- y usa ese tiempo para conocer cada nota nueva
antes de que suene: una nota nunca sale con el intervalo de la anterior. Las notas
se reconocen desde el Mi grave (y afinaciones drop) hasta el traste 24, con un
error de pocos cents, en unos 25 ms (45 ms en las cuerdas más graves). Los bendings
y el vibrato se siguen de forma continua: en un bending de Do a Re en Do mayor la
armonía se desliza de Mi a Fa. Las notas fuera de la tonalidad (una blue note, el
Sol# de La menor) toman el grado de la escala que da una tercera o quinta real:
Sol# recibe Si, Sib en Do mayor recibe Re.

**Mandos en modo HARMONIZER**: **MIX** equilibra la armonía con la nota que tocas,
que siempre se mantiene (100 % = las dos al mismo nivel, 0 % = sin armonía);
**FINE** desafina ligeramente la armonía para un sonido más ancho; **LEVEL** funciona
como siempre. SEMITONES, WINDOW y FEEDBACK descansan. TYPE elige el carácter de la
voz: **Studio**, **Low Latency** (menos retraso; en frases muy rápidas puede perder
algo de precisión en notas graves) y **Vintage** (más oscura). El bloque del rack
indica **HARMONY** mientras el armonizador está activo.

Toca notas sueltas: las terceras y quintas siguen melodías, riffs y solos. Los
acordes confunden cualquier detección de nota, así que simplemente suenan sin
armonía. La detección usa la señal limpia de la guitarra, antes de la ganancia, el
NAM y los efectos. Los ajustes de HARMONIZER se guardan con el bloque PITCH y
siguen un enlace L / R.
