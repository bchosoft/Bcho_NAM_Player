# Bcho NAM Player

[English](README.md)

![Bcho NAM Player](docs/Caratula_BNAMP.png)

Bcho NAM Player es un procesador de guitarra standalone y portable desarrollado en C++20 con JUCE 8 y Neural Amp Modeler Core. Combina reproducción de modelos NAM A1/A2, impulsos de pantalla, efectos orientados a estudio, enrutamiento flexible, afinador estable y la interfaz fotorrealista del amplificador Bcho.

## Release 1.0.0

Esta versión incluye el frontal standalone completo, la puerta de ruido profesional y el navegador rediseñado de NAM e IR. Input Cali muestra ahora un pequeño LED verde cuando la calibración automática está activa; utiliza la referencia de la interfaz seleccionada y aplica +12 dBu cuando el NAM no contiene metadatos de entrada. El paquete inicial no incluye archivos IR, por lo que el bloque IR comienza desactivado hasta cargar una respuesta de pantalla. Ambos manuales se incluyen en español e inglés.

## Descarga

Descarga los paquetes actuales desde la [última release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest):

- **Windows x64:** ZIP portable con `BchoNAMPlayer.exe`, ASIO/WASAPI y todos los recursos necesarios.
- **macOS Apple Silicon:** ZIP para Macs `arm64` (M1/M2/M3 y posteriores).
- **macOS Intel:** ZIP para Macs `x86_64`.
- **Linux x86_64:** ZIP con un AppImage portable.
- `SHA256SUMS.txt` permite verificar todos los ZIP descargados.

Conserva junto todo el contenido del ZIP. Cada paquete incluye dos modelos NAM de demostración en `Models`; las IR no se incluyen inicialmente.

## Funciones principales

- Detección automática de la arquitectura NAM A1/A2.
- Bloques móviles COMP, DELAY, CHORUS, FLANGER, PHASER, REVERB, OCTAVER y PITCH.
- Segundo modelo NAM opcional como pedal de overdrive o distorsión.
- Enrutamiento mediante arrastre antes del PREAMP, en el loop/pre-IR o después del IR.
- Gate profesional, tonestack de cuatro bandas, convolución de IR y mezcla dry/IR.
- Afinador sobre la señal DI intacta y selección de afinaciones alternativas.
- Rutas de salida MAIN, PRE, DI y WET en la configuración de audio del standalone.
- Presets portables `.bnpp` que incorporan el NAM principal, el pedal NAM opcional, IR, orden de efectos y todos los ajustes.
- Ajustes desde la rueda dentada: skins con previsualización y aplicación confirmada, versión instalada y búsqueda manual o automática de actualizaciones.
- Listas NAM e IR iguales, con cuatro filas visibles, scroll, flechas de navegación y drag-and-drop.
- Selección de carpetas para NAM e IR, selección automática del primer elemento, mensajes claros cuando no se encuentra el tipo de archivo y fade al cambiar de modelo o IR.
- Doble clic en los potenciómetros para recuperar sus valores iniciales: las 12 en punto en los controles normales y totalmente a la izquierda/apagado en Gate.
- LED de estado de Input Cali junto al interruptor: verde cuando está activado y apagado cuando está desactivado.

## Instalación

### Windows

Descomprime el ZIP en una carpeta con permisos de escritura y ejecuta `BchoNAMPlayer.exe`. En **AUDIO SETUP** selecciona el sistema de audio, interfaz, canales habilitados, frecuencia de muestreo, buffer y rutas de salida. Para utilizar ASIO instala el controlador oficial del fabricante de tu interfaz.

### macOS

Descomprime el ZIP y abre `BchoNAMPlayer.app`. Los paquetes de macOS todavía no están firmados ni notarizados; en el primer inicio haz clic derecho sobre la aplicación y selecciona **Abrir** si Gatekeeper solicita confirmación.

### Linux

Descomprime el ZIP, concede permiso de ejecución al AppImage si fuera necesario y ábrelo:

```bash
chmod +x BchoNAMPlayer-*.AppImage
./BchoNAMPlayer-*.AppImage
```

La disponibilidad de ALSA/JACK y los permisos de audio en tiempo real dependen de la distribución y de la configuración del usuario.

## Navegación de NAM e IR

Usa **BROWSE NAM** o arrastra un `.nam` al bloque PreAmp/Amp o a la lista. Usa **BROWSE IR** o arrastra un `.wav` al bloque IR o a la lista. Las flechas recorren los archivos de la carpeta actual. El bloque IR comienza desactivado hasta cargar una respuesta impulsional.

## Señal y enrutamiento de salidas

La ruta MAIN normal está completamente procesada y con los controles por defecto es neutra. PRE siempre entrega el resultado del NAM principal sin el procesamiento del player; DI entrega la entrada intacta de la interfaz; WET permite grabar una rama procesada independiente. La configuración del dispositivo de audio permanece local al standalone y no se guarda en los presets `.bnpp`.

## Notas

- Versión: 1.0.0.
- Windows: x64, Windows 10/11.
- macOS: Apple Silicon `arm64` o Intel `x86_64`, macOS 11 o posterior.
- Linux: AppImage x86_64.
- Bcho NAM Player no distribuye capturas NAM de terceros. Respeta la licencia de cada modelo e IR utilizado.

Consulta los [avisos de terceros](THIRD_PARTY_NOTICES.md) para conocer las licencias del framework y sus dependencias.
