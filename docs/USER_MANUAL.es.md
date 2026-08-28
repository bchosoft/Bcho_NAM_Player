# Bcho NAM Player — Manual de usuario

## 1. Qué es

Bcho NAM Player es un procesador de guitarra portable para Windows, macOS y Linux. Reproduce modelos Neural Amp Modeler (`.nam`), respuestas impulsionales (`.wav`) y una cadena de efectos reordenable. La edición standalone controla también la interfaz de audio; la edición VST3 recibe el audio y la configuración del DAW.

## 2. Instalación rápida

Descarga el ZIP de tu sistema desde la [última release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest) y conserva juntos todos sus archivos.

- Windows: ejecuta `BchoNAMPlayer.exe`.
- macOS: usa `BchoNAMPlayer.app`; elige el paquete Intel o Apple Silicon.
- Linux: ejecuta el AppImage y dale permiso de ejecución si es necesario.

Los modelos NAM y las IR no se distribuyen con la aplicación. Carga tus propios archivos desde la pantalla central. En macOS los paquetes no están firmados ni notarizados.

## 3. Panel principal

El cabezal contiene, de izquierda a derecha, el interruptor **POWER**, los controles de entrada, el afinador, los controles del amplificador y los vúmetros. La pantalla central muestra el modelo activo, el nivel calibrado, la salida, el archivo IR y los controles de carga/borrado.

Todos los potenciómetros usan el mismo mando metálico. Arrástralos verticalmente u horizontalmente para cambiar el valor. Un doble clic devuelve el control a su valor inicial: todos quedan a las 12 en punto salvo **Gate**, que vuelve a 0 y deja la puerta desactivada.

### Controles de entrada y amplificador

- **POWER**: activa o silencia el procesamiento principal.
- **Input Gain**: ajusta el nivel que entra al modelo NAM.
- **Input Cali (Auto)**: compensa automáticamente el nivel de entrada cuando el modelo contiene el metadato `input_level_dbu`. Si el modelo no lo contiene, no aplica corrección.
- **Gate**: puerta de ruido profesional. En 0 está completamente desactivada. Al subirlo aumenta el umbral; el detector usa envolvente suavizada, ataque, mantenimiento y liberación para evitar cortes bruscos.
- **Bass, Mid, Treble, Presence**: ecualización de cuatro bandas después del preamplificador NAM.
- **IR Blend**: mezcla la señal procesada sin IR con la señal convolucionada por la respuesta impulsional.
- **Master Vol**: nivel principal después de la cadena del reproductor.
- **Output Gain**: ganancia final de salida.

Con los valores por defecto, la ruta MAIN es neutra y suena igual que PRE. La ruta PRE es una referencia independiente y nunca cambia al mover controles del reproductor.

## 4. Afinador

Activa el interruptor **TUNER**. El afinador analiza siempre la señal DI limpia, antes de la puerta, el NAM y los efectos. Las luces indican si la nota está baja, afinada o alta; la nota detectada aparece debajo. Permite elegir afinación estándar y alternativas. Para una lectura estable, toca una cuerda aislada con nivel suficiente y deja que desaparezca el ruido entre notas.

## 5. Modelos NAM e IR

Haz clic en el perfil de la pantalla central para seleccionar un archivo `.nam`. La arquitectura A1/A2 se detecta automáticamente; no hay que elegirla manualmente. Al cargar otro NAM, los controles y switches vuelven a sus valores por defecto.

La lista **IR FILES** busca archivos `.wav` en la carpeta `IRs` situada junto al ejecutable. Selecciona una IR y pulsa **LOAD IR**. **DELETE** elimina la IR activa. Las IR mono y estéreo se preparan para la frecuencia de audio seleccionada.

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

## 8. Presets `.bnpp`

**SAVE .BNPP** crea un preset portable autocontenido. Incluye el XML de estado, el NAM principal, el NAM de pedal opcional, la IR, el orden del rack, tipos, bypasses y todos los controles. **LOAD .BNPP** extrae sus recursos a una caché segura y restaura la configuración. La configuración de audio no se incluye para que el preset pueda viajar entre ordenadores y DAW.

## 9. Estado y solución de problemas

La aplicación recupera el último NAM, IR y preset utilizado. Si no hay audio, revisa POWER, el dispositivo seleccionado, las entradas activas, el buffer y el nivel del vúmetro INPUT. Si el NAM no suena, comprueba que el archivo sea válido y que su licencia permita su uso. Para reducir latencia empieza con un buffer ASIO pequeño y súbelo si aparecen clics.

