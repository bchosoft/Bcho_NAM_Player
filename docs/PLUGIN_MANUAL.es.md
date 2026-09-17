# Bcho NAM Player 1.7.0 - Manual plugin VST3 / AU

## 1. Qué incluye

Plugin de efecto de audio, no instrumento MIDI. Dos rutas L/R con dos bloques NAM, IR y rack por ruta. VST3 en Windows x64, macOS Intel/Apple Silicon y Linux x86_64. AU únicamente en macOS. Usa el paquete que coincida con la arquitectura del DAW. No se incluye AAX.

## 2. Instalación

Cierra el DAW antes de copiar. Copia el paquete completo, no solo el binario de su interior.

- Windows: copia la carpeta Bcho NAM Player.vst3 en C:/Program Files/Common Files/VST3. Puede pedir permisos de administrador.
- macOS VST3: copia Bcho NAM Player.vst3 en ~/Library/Audio/Plug-Ins/VST3.
- macOS AU: copia Bcho NAM Player.component en ~/Library/Audio/Plug-Ins/Components.
- Linux: copia Bcho NAM Player.vst3 en ~/.vst3.

Inicia el DAW y vuelve a escanear plugins. Aparece como Bcho NAM Player. Usa VST3 en un host compatible o AU en un host Audio Unit, como Logic. Instala solo la arquitectura del proceso del DAW: Intel x86_64 o Apple Silicon arm64. Las compilaciones macOS tienen firma ad-hoc y no están notarizadas. Si macOS las bloquea, revisa Privacidad y seguridad y las instrucciones del host; no desactives globalmente las protecciones del sistema.

## 3. Primera pista

Añade el plugin como efecto en una pista de audio mono o estéreo. Selecciona tu entrada de guitarra en el DAW y activa monitorización. Empieza con niveles bajos y evita monitorización doble por interfaz y DAW.

Una instancia nueva empieza en MONO con todos los bloques desactivados. Pasa señal seca hasta cargar o activar procesamiento. POWER permite silenciar la ruta. Dispositivo, driver, frecuencia y buffer se configuran en el DAW, no en el plugin.

MONO procesa la ruta L y envía su resultado a las salidas del plugin. En un bus estéreo, STEREO procesa entrada L y R por separado. Para una guitarra con dos cadenas en estéreo, duplica/envía la señal a ambos canales desde el DAW. El selector DUAL MONO / SPLIT L/R del standalone no está en el plugin.

## 4. Cargar modelos y pantallas

Selecciona NAM 1 L o NAM 2 L; en estéreo también NAM 1 R o NAM 2 R. Usa BROWSE LOCAL o arrastra un archivo compatible .nam. Cada bloque acepta modelos NAM compatibles y se activa al cargarlos. NAM 1 y NAM 2 conservan controles de tono independientes.

Selecciona IR L o IR R y usa BROWSE IR para una respuesta .wav. No se incluyen IR. Su nivel no se normaliza. IR BLEND mezcla señal seca y cabina; IR VOL ajusta la parte de cabina entre -24 y 0 dB. El fader indica L/R y deja la escala fuera del mando. Cargar una respuesta la activa; desactiva su bloque para comparar.

Las capturas de demostración se incluyen en Models junto al paquete, pero no se cargan automáticamente. Usa BROWSE LOCAL para encontrarlas. No muevas recursos de un proyecto sin guardarlos o consolidarlos antes.

## 5. Controles y efectos

INPUT GAIN y OUTPUT GAIN controlan entrada/salida; GATE la puerta; MASTER VOL el nivel principal. BASS, MID, TREBLE y PRESENCE siguen al NAM seleccionado. IR BLEND e IR VOL siguen al selector IR. Los vúmetros permiten comprobar entrada y salida.

Cada ruta tiene compresor, octavador, pitch shifter, chorus, flanger, phaser, delay y reverb. Pulsa un bloque para activar/bypass; doble clic abre editor o carga. Arrastra para ordenar respetando los anclajes NAM 2 e IR. Cada efecto convencional dispone de tres algoritmos y seis parámetros. Los cambios suavizados evitan transiciones bruscas, pero no sustituyen una buena gestión de niveles.

TUNER analiza DI. Toca una cuerda aislada; el indicador central muestra afinación. INPUT CALI utiliza la referencia interna del motor y los metadatos del modelo; el plugin no ofrece el ajuste de referencia de interfaz de Audio Setup. Si necesitas una calibración concreta de tu interfaz, ajusta ganancia externamente o usa el standalone.

## 6. Guardado y automatización

Guarda el proyecto del DAW para conservar ambas rutas, parámetros, rutas de archivos y estados/orden del rack. El estado del DAW referencia los NAM/IR en disco: NO incrusta automáticamente esos archivos. Deben seguir disponibles al reabrir o trasladar el proyecto.

SAVE PRESET crea un .bnpp de la ruta seleccionada con NAM 1, NAM 2, IR y ajustes. LOAD PRESET sustituye esa ruta. Para compartir ambas rutas, guarda un preset por lado; para recuperar toda la instancia utiliza el proyecto del DAW. Al importar un preset de dos rutas del standalone, el plugin utiliza la representación compatible de la ruta izquierda en la ruta seleccionada.

El DAW puede automatizar los parámetros publicados, incluidos ganancias, tono, mezcla, IR VOL, encendido, calibración, afinador y MONO/STEREO. No todos los controles del rack son parámetros de automatización del host: orden, algoritmos y ajustes internos se guardan en el estado. Cambios de archivo requieren una carga y no deben tratarse como automatización continua.

## 7. TONE3000 y WebView2

TONE3000 abre la biblioteca de favoritos, descargados, novedades, tendencias y capturas propias. Conecta la cuenta y usa SEARCH FULL CATALOGUE para el buscador oficial. Acceso y búsqueda integrados comparten sesión. El servicio puede pedir reautenticación si caduca.

Windows comprueba WebView2: si falta o no está disponible ofrece descarga oficial de Microsoft, navegador externo o cancelar. No hay instalación automática ni se incluye su instalador en el ZIP. Instálalo desde Microsoft y reabre TONE3000. El audio local no depende de WebView2. macOS usa WKWebView y Linux el navegador externo. La red, autenticación y disponibilidad del catálogo dependen del servicio externo.

## 8. Diferencias con standalone

El plugin utiliza el acabado Astra / Obsidian. No contiene las once skins seleccionables, la configuración de dispositivo, las salidas físicas MAIN/PRE/DI/WET ni el selector de entradas dual del standalone. Enruta y configura desde el DAW. Una instancia nueva no hereda la última sesión standalone; una instancia guardada se recupera desde el proyecto del host.

## 9. Problemas habituales

- No aparece: revisa carpeta, arquitectura y formato; vuelve a escanear.
- Sin sonido: revisa entrada, monitorización, POWER y rutas del DAW.
- Solo un lado: en STEREO comprueba que el DAW alimente ambos canales.
- Recursos ausentes: restaura sus ubicaciones o carga tus presets .bnpp.
- Chasquidos: aumenta buffer y reduce carga; dos cadenas con cuatro NAM pueden exigir más CPU.
- TONE3000 vacío: revisa conexión, cuenta y WebView2; prueba navegador externo.
- El host bloquea un plugin macOS: revisa su validación y los permisos del sistema. La firma ad-hoc no equivale a notarización.

## 10. Integridad y licencias

Verifica el ZIP con SHA256SUMS.txt. Consulta THIRD_PARTY_NOTICES.md. Respeta las licencias de los NAM e IR incluidos en tus presets. Los manuales no implican certificación en todos los DAW; las combinaciones host/sistema requieren validación práctica.
