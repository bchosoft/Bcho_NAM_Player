# Bcho NAM Player — Manual de usuario

## 1. Qué es

Bcho NAM Player es un procesador de guitarra portable para Windows, macOS y Linux. Reproduce modelos Neural Amp Modeler (`.nam`), respuestas impulsionales (`.wav`) y una cadena de efectos reordenable. La edición standalone controla también la interfaz de audio; la edición VST3 recibe el audio y la configuración del DAW.

## 2. Instalación rápida

Descarga el ZIP de tu sistema desde la [última release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest) y conserva juntos todos sus archivos.

- Windows: ejecuta `BchoNAMPlayer.exe`.
- macOS: usa `BchoNAMPlayer.app`; elige el paquete Intel o Apple Silicon.
- Linux: ejecuta el AppImage y dale permiso de ejecución si es necesario.

El paquete inicial incluye dos modelos NAM de demostración en `Models`; no incluye IRs. Puedes añadir tus propios modelos e IR desde la pantalla central o arrastrándolos desde el explorador. En macOS los paquetes no están firmados ni notarizados.

## 3. Panel principal

El cabezal contiene, de izquierda a derecha, el interruptor **POWER**, los controles de entrada, el afinador, los controles del amplificador y los vúmetros. La pantalla central se divide en dos zonas iguales: **NAM MODELS** e **IR FILES**. Cada lista muestra cuatro elementos y añade scroll cuando hay más.

Todos los potenciómetros usan el mismo mando metálico. Arrástralos verticalmente u horizontalmente para cambiar el valor. Un doble clic devuelve el control a su valor inicial: todos quedan a las 12 en punto salvo **Gate**, que vuelve a 0 y deja la puerta desactivada.

### Controles de entrada y amplificador

- **POWER**: activa o silencia el procesamiento principal.
- **Input Gain**: ajusta el nivel que entra al modelo NAM.
- **Input Cali (Auto)**: compara la referencia configurada de la interfaz con el metadato `input_level_dbu` del modelo. Si el metadato no existe, utiliza la referencia NAM estándar de +12 dBu.
- **Gate**: puerta de ruido profesional. En 0 está completamente desactivada. Al subirlo aumenta el umbral; el detector usa envolvente suavizada, ataque, mantenimiento y liberación para evitar cortes bruscos.
- **Bass, Mid, Treble, Presence**: ecualización de cuatro bandas después del preamplificador NAM.
- **IR Blend**: mezcla la señal procesada sin IR con la señal convolucionada por la respuesta impulsional.
- **Master Vol**: nivel principal después de la cadena del reproductor.
- **Output Gain**: ganancia final de salida.

Con los valores por defecto, la ruta MAIN es neutra y suena igual que PRE. La ruta PRE es una referencia independiente y nunca cambia al mover controles del reproductor.

## 4. Afinador

Activa el interruptor **TUNER**. El afinador analiza siempre la señal DI limpia, antes de la puerta, el NAM y los efectos. Las luces indican si la nota está baja, afinada o alta; la nota detectada aparece debajo. Permite elegir afinación estándar y alternativas. Para una lectura estable, toca una cuerda aislada con nivel suficiente y deja que desaparezca el ruido entre notas.

## 5. Modelos NAM e IR

Usa **BROWSE NAM** o arrastra un `.nam` a la lista central o al bloque **PreAmp/Amp (NAM Model)**. La arquitectura A1/A2 se detecta automáticamente; no hay que elegirla manualmente. También puedes navegar con las flechas arriba/abajo. **TONE3000** abre el buscador online y carga el modelo seleccionado. Al cargar otro NAM, los controles y switches vuelven a sus valores por defecto.

Usa **BROWSE IR** o arrastra un `.wav` a la lista central o al bloque **IR**. La lista muestra los archivos de la carpeta donde se encuentra la IR seleccionada; las flechas permiten navegar por esa carpeta. El bloque IR permanece desactivado si no hay una IR cargada. Las IR mono y estéreo se preparan para la frecuencia de audio seleccionada.

## 6. Rack de efectos

El rack se abre sobre el cabezal. Arrastra los bloques para cambiar su posición y haz clic para activar o poner en bypass. Doble clic abre la ventana avanzada; se cierra con **X**, Escape o haciendo clic fuera.

Los anclajes **PREAMP** e **IR** indican la posición eléctrica. Un efecto antes de PREAMP equivale a un pedal delante del amplificador; entre PREAMP e IR equivale al loop; después de IR es post-cabina. El afinador no aparece en el rack porque siempre va primero. **NAM FX** permite añadir un segundo NAM como pedal de overdrive o distorsión.

Cada bloque tiene tres algoritmos y seis parámetros:

| Bloque | Tipos | Parámetros |
|---|---|---|
| COMPRESSOR | Studio VCA, Optical, FET Punch | Threshold, Ratio, Attack, Release, Makeup, Mix |
| DELAY | Digital Studio, Tape Echo, Analog BBD | Time, Feedback, Mix, Tone, Mod, Level |
| CHORUS | Studio, Ensemble, Tri-Chorus | Rate, Depth, Mix, Delay, Feedback, Level |
| FLANGER | Analog, Through-Zero, Jet | Rate, Depth, Mix, Feedback, Manual, Level |
| PHASER | 4 Stage, 8 Stage, 12 Stage | Rate, Depth, Mix, Feedback, Centre, Level |
| REVERB | Studio Room, Plate, Concert Hall | Size, Damping, Mix, Width, Freeze, Level |
| OCTAVER | Poly Clean, Classic Mono, Organ | Oct Down, Oct Up, Dry, Tone, Tracking, Level |
| PITCH SHIFTER | Studio, Low Latency, Vintage | Semitones, Mix, Window, Feedback, Fine, Level |

Los valores se muestran con sus unidades en la pantalla del bloque. Los cambios de bypass, parámetros y tipo se suavizan para evitar clics; los delays utilizan interpolación y las realimentaciones están limitadas para mantener el procesamiento estable.

## 7. AUDIO SETUP — solo standalone

Abre **AUDIO SETUP** para elegir:

- sistema de audio y driver, incluido ASIO en Windows;
- interfaz de entrada/salida;
- entradas y salidas activas;
- frecuencia de muestreo y tamaño de buffer;
- panel de control del fabricante cuando está disponible;
- enrutamiento de salidas.

Las rutas disponibles son **MAIN** (procesada), **PRE** (NAM sin controles ni efectos del player), **DI** (entrada limpia) y **WET** (rama procesada posterior a la cabina). MAIN se dirige por defecto a las salidas 1/2 cuando están habilitadas. La última configuración de dispositivo y ruteo se recupera al iniciar de nuevo. El VST3 no muestra esta ventana porque el DAW gestiona el audio.

## 8. Ajustes, skins y actualizaciones

Pulsa la rueda dentada situada en la esquina derecha de la cabina para abrir **SETTINGS**. Desde ahí puedes:

- elegir temporalmente una skin para previsualizarla; la skin solo queda aplicada al pulsar **APPLY**;
- elegir otra skin instalada que mantenga las posiciones exactas de pantallas, potenciómetros, escalas y switches;
- consultar la versión instalada;
- usar **CHECK FOR UPDATES** para buscar manualmente una nueva versión;
- activar o desactivar **CHECK ON STARTUP**, la comprobación automática al iniciar. El estado se indica con un LED discreto y la opción está oculta en Settings para no invadir el frontal.

La búsqueda de actualizaciones solo informa de versiones publicadas; no cambia el preset, los modelos ni el audio sin confirmación del usuario. El VST3 conserva los controles, tuner, pantalla central, rack y skins, pero no muestra **AUDIO SETUP**, porque el DAW gestiona el dispositivo.

## 9. Presets `.bnpp`

**SAVE .BNPP** crea un preset portable autocontenido. Incluye el XML de estado, el NAM principal, el NAM de pedal opcional, la IR, el orden del rack, tipos, bypasses y todos los controles. **LOAD .BNPP** extrae sus recursos a una caché segura y restaura la configuración. La configuración de audio no se incluye para que el preset pueda viajar entre ordenadores y DAW.

## 10. Estado y solución de problemas

La aplicación recupera el último NAM, IR y preset utilizado. Si no hay audio, revisa POWER, el dispositivo seleccionado, las entradas activas, el buffer y el nivel del vúmetro INPUT. Si el NAM no suena, comprueba que el archivo sea válido y que su licencia permita su uso. Para reducir latencia empieza con un buffer ASIO pequeño y súbelo si aparecen clics.
