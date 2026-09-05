# Bcho NAM Player 1.6.0 - Manual de usuario

## 1. Descripción

Bcho NAM Player 1.6.0 es un procesador de guitarra standalone y portable para Windows, macOS y Linux. Reproduce capturas Neural Amp Modeler (`.nam`), respuestas impulsionales de pantalla (`.wav`) y una cadena reordenable de efectos de estudio. La aplicación standalone controla el dispositivo de audio, el ruteo y la latencia.

Esta versión añade una interfaz fotorrealista responsive, pestañas independientes para las listas BLOCK NAM 1 y BLOCK NAM 2, activación automática al cargar un NAM compatible, búsqueda profunda de carpetas, volumen independiente de la cabina IR, respuesta visual de los altavoces según la salida real, fondo de backstage a pantalla completa y once skins coordinadas.

La ventana inicial utiliza el tamaño nativo de 1537 x 1023 siempre que lo permita el área disponible de la pantalla y aparece centrada. Todo el diseño es responsive: mueble, controles, listas, vúmetros y textos se escalan juntos. La ventana no puede reducirse por debajo del 50 por ciento para evitar que controles o serigrafías salgan de su zona.

## 2. Instalación

Descarga el paquete correspondiente desde la [última release pública](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest), descomprímelo y conserva juntos todos los archivos y carpetas incluidos.

- **Windows x64**: ejecuta `BchoNAMPlayer.exe`. Instala el driver ASIO oficial del fabricante cuando esté disponible.
- **macOS Apple Silicon**: usa el ZIP `arm64` y abre `BchoNAMPlayer.app`.
- **macOS Intel**: usa el ZIP `x86_64` y abre `BchoNAMPlayer.app`.
- **Linux x86_64**: ejecuta el AppImage. Si no tiene permiso, usa `chmod +x BchoNAMPlayer-*.AppImage`.

Las aplicaciones macOS usan firma ad-hoc pero no están notarizadas. En el primer inicio haz clic derecho y selecciona **Abrir** si Gatekeeper pide confirmación.

El paquete incluye dos modelos NAM de demostración en `Models`. No contiene ninguna IR de pantalla. Por eso el bloque IR comienza en bypass hasta cargar una respuesta.

## 3. Panel frontal

El rack superior contiene los botones de preset, los bloques reordenables, el botón/pantalla del afinador y el selector de afinación. El cabezal contiene siete controles principales, vúmetros LED verticales simétricos, ganancias de entrada/salida, Input Cali, navegadores separados de NAM e IR, Settings y el interruptor rojo de encendido. La cabina muestra el logotipo Bcho y dos conos animados.

### Manejo de los potenciómetros

Arrastra un pote vertical u horizontalmente para modificarlo. El valor exacto aparece debajo. Un doble clic recupera el valor inicial: los controles normales vuelven a las 12 y Gate vuelve totalmente a la izquierda, en **OFF**.

### Controles principales

- **POWER**: activa o silencia la ruta principal. El switch se ilumina en rojo cuando está encendido.
- **INPUT GAIN**: ajusta la señal que entra a la cadena de procesamiento NAM.
- **GATE**: puerta de ruido profesional. En 0 está completamente fuera de la ruta. Al subirlo aumenta el umbral; ataque, mantenimiento y liberación suavizados evitan cortes bruscos.
- **BASS, MID, TREBLE, PRESENCE**: ecualización de cuatro bandas después del NAM.
- **MASTER VOL**: nivel principal posterior al procesamiento.
- **IR BLEND**: mezcla la señal sin convolución y la procesada mediante IR.
- **IR CABINET VOLUME**: fader vertical de ganancia independiente de la cabina húmeda antes de IR Blend, ajustable entre -24 dB y 0 dB. Comienza en -12 dB para dejar margen con IR de nivel alto. La escala y el valor actual en dB aparecen junto al fader.
- **OUTPUT GAIN**: nivel final de salida.
- **INPUT VU / OUTPUT VU**: vúmetros LED de colores para la entrada y la salida final.

El player aplica un fade protector al restaurar el estado inicial y al cargar un NAM o una IR. Esto evita clics o crujidos durante la transición.

## 4. Movimiento de los conos

Los dos conos responden visualmente al nivel RMS final real. Tocar más fuerte o aumentar Master Volume/Output Gain produce mayor recorrido; el silencio o apagar POWER los devuelve suavemente al reposo.

Solo se mueve la superficie interior. Aros, tornillos, rejilla, cabina y logotipo permanecen fijos. La animación se calcula a 60 fotogramas por segundo en el hilo gráfico y nunca modifica, retrasa ni realimenta la señal de audio.

## 5. Carga de modelos NAM

Usa **BROWSE NAM** para seleccionar un `.nam` o una carpeta. Al elegir una carpeta, se añaden a la lista todos sus NAM y se selecciona automáticamente el primero. Si no encuentra ninguno, la aplicación muestra **NAM file not found**.

La lista NAM muestra cuatro filas al tamaño nativo, añade scroll cuando es necesario y usa las flechas para seleccionar el elemento anterior o siguiente. Cada flecha se desactiva al llegar a su extremo. **TONE3000** abre el navegador online y carga el modelo descargado con su nombre descriptivo.

La aplicación identifica automáticamente NAM A1, A2 Standard y A2 Nano. No existe un selector manual de arquitectura. Cargar un modelo en BLOCK NAM 2 devuelve frontal y rack a valores seguros, activa BLOCK NAM 2, mantiene activa la cabina IR seleccionada y usa un fade antirruido.

### Drag-and-drop

Arrastra un `.nam` o una carpeta a su lista NAM o directamente al bloque **BLOCK NAM 2**. Se utilizan el mismo escaneo y los mismos mensajes de error que con BROWSE LOCAL.

## 6. BLOCK NAM 1 y BLOCK NAM 2

Ambos bloques aceptan cualquier `.nam` compatible; la aplicación no presupone qué equipo se capturó. Usa la pestaña correspondiente, **+ BLOCK NAM 1**, haz doble clic en cualquiera de los bloques NAM o arrastra el archivo/carpeta directamente sobre su pestaña o bloque. El origen puede ser local o TONE3000. Cargar un modelo válido activa ese bloque.

BLOCK NAM 1 y BLOCK NAM 2 son independientes. Cada pestaña conserva su carpeta, modo de búsqueda profunda, lista y selección. Poner uno en bypass elimina únicamente esa etapa NAM.

## 7. Carga de IR

Usa **BROWSE IR** para seleccionar un `.wav` o una carpeta. La carpeta se filtra para localizar WAV cortos adecuados como respuestas impulsionales, se listan los válidos y se selecciona el primero. Si no se encuentra ninguno, aparece **IR not found**.

La lista IR tiene el mismo tamaño y navegación que la lista NAM. Arrastra un WAV o una carpeta a la lista IR o al bloque **IR** para usar el mismo cargador. Las respuestas mono y estéreo se preparan para la frecuencia activa. Se conserva su ganancia original: Bcho NAM Player no normaliza las IR.

Pulsa de nuevo la IR seleccionada para deseleccionarla. Se elimina la respuesta activa y el bloque queda en bypass. Cargar o cambiar de IR usa una transición antirruido. Usa **IR CABINET VOLUME** para ajustar independientemente el nivel de la cabina húmeda sin modificar la mezcla seco/húmedo de **IR BLEND**.

## 8. Rack y orden de señal

Arrastra horizontalmente los bloques para cambiar el orden. **BLOCK NAM 2** e **IR** son anclajes eléctricos:

- Antes de **BLOCK NAM 2**: procesamiento anterior a la segunda etapa NAM.
- Entre **BLOCK NAM 2** e **IR**: procesamiento pre-cabina.
- Después de **IR**: procesamiento posterior a la pantalla.

El afinador siempre ocupa el primer lugar sobre la DI intacta y no pertenece al orden arrastrable. Un clic activa o pone en bypass. Un doble clic abre el editor o cargador sin interpretar el primer clic como cambio de bypass.

Cada efecto convencional dispone de tres algoritmos y seis parámetros:

| Bloque | Algoritmos | Parámetros |
|---|---|---|
| COMP | Studio VCA, Optical, FET Punch | Threshold, Ratio, Attack, Release, Makeup, Mix |
| DELAY | Digital Studio, Tape Echo, Analog BBD | Time, Feedback, Mix, Tone, Mod, Level |
| CHOR | Studio, Ensemble, Tri-Chorus | Rate, Depth, Mix, Delay, Feedback, Level |
| FLANG | Analog, Through-Zero, Jet | Rate, Depth, Mix, Feedback, Manual, Level |
| PHASE | 4 Stage, 8 Stage, 12 Stage | Rate, Depth, Mix, Feedback, Centre, Level |
| REVERB | Studio Room, Plate, Concert Hall | Size, Damping, Mix, Width, Freeze, Level |
| OCT | Poly Clean, Classic Mono, Organ | Oct Down, Oct Up, Dry, Tone, Tracking, Level |
| PITCH | Studio, Low Latency, Vintage | Semitones, Mix, Window, Feedback, Fine, Level |

Los cambios de parámetro, tipo y bypass se suavizan. Las lecturas de delay están interpoladas y las realimentaciones limitadas para garantizar estabilidad.

## 9. Afinador

Pulsa **TUNER** para activarlo. El texto se ilumina en verde y el botón simula estar presionado. La pantalla muestra la nota detectada y una indicación LED izquierda/derecha para baja, centrada o alta.

El afinador analiza la DI intacta antes de Gate, NAM y efectos. Cubre aproximadamente 65 a 700 Hz con frecuencias habituales entre 44,1 y 192 kHz. Las afinaciones disponibles son Standard, Drop D, D Standard, Eb y Open G. Toca una cuerda aislada con nivel suficiente y deja caer el ruido entre notas.

## 10. Input Cali

Input Cali compensa la relación entre el nivel máximo de entrada de la interfaz y la referencia utilizada al entrenar el NAM.

Configura **Interface Input Reference / 0 dBFS Peak** en Audio Setup. Al activar Input Cali se calcula:

`ganancia de calibración en dB = referencia dBu de la interfaz - referencia dBu del NAM`

- Si el NAM contiene `input_level_dbu`, se utiliza ese metadato.
- Si no tiene metadatos, se presupone la referencia NAM probable de +12 dBu.
- La corrección se limita entre -24 y +24 dB.
- Para una PreSonus Studio 24c introduce +10 dBu.
- El pequeño LED junto a INPUT CALI se ilumina en verde cuando está activado y se apaga al desactivarlo.

Input Cali modifica la ganancia antes del NAM; no reescribe ni normaliza el modelo. Si la interfaz ofrece varios modos de ganancia, usa el dBu correspondiente al modo físico de entrada utilizado.

## 11. Audio Setup y ruteo

Abre la rueda dentada y elige **AUDIO SETUP**. El panel controla:

- sistema y driver, incluido ASIO en Windows;
- interfaz de entrada/salida;
- canales activos;
- frecuencia de muestreo y buffer;
- panel del fabricante cuando el driver lo ofrece;
- referencia de entrada utilizada por Input Cali;
- destinos físicos MAIN, PRE, DI y WET.

| Ruta | Señal | Uso habitual |
|---|---|---|
| MAIN | Salida completa procesada | Monitorización o grabación final |
| PRE | BLOCK NAM 2 antes de tono/efectos/cabina | Reamping o comparación |
| DI | Entrada intacta de la interfaz | Pista limpia de seguridad |
| WET | Rama procesada post-cabina | Grabación procesada independiente |

MAIN utiliza normalmente las salidas 1/2. Desactiva una ruta no utilizada para evitar duplicados. Dispositivo, canales, frecuencia, buffer, referencia y ruteo se restauran al iniciar de nuevo.

## 12. Presets portables `.bnpp`

**SAVE .BNPP** crea un preset autocontenido con:

- modelo de BLOCK NAM 2;
- modelo de BLOCK NAM 1, si está cargado;
- IR seleccionada opcional;
- orden, algoritmos, parámetros y bypasses del rack;
- potenciómetros, switches y ajustes del afinador.

Los recursos se verifican mediante SHA-256 al cargarlos. **LOAD .BNPP** los extrae en la caché de la aplicación y restaura el sonido. Dispositivo, interfaz y salidas físicas se excluyen para que el preset pueda trasladarse entre ordenadores.

Debe existir un modelo cargado en BLOCK NAM 2 antes de guardar un `.bnpp`.

## 13. Settings, skins y actualizaciones

Settings se abre desde la rueda dentada situada a la derecha de Reverb, en el
rack superior. La reconstrucción actual añade placas metálicas de montaje y
marcos coordinados con cada acabado, mandos propios de cada skin y un fondo de
backstage que llena toda la ventana al maximizarla. IR VOL tiene una placa
independiente de la misma altura que los paneles de archivos.

La colección incluye además **Classic Black / Levant Tolex**, sumando once
acabados en el standalone. Los materiales quedan expuestos, sin placas
transparentes superpuestas. Cada módulo lleva esquineras metálicas; el rack
también las lleva abajo. Las serigrafías usan contraste adaptado al acabado.

Pulsa la rueda dentada para abrir **APPLICATION SETTINGS**. Contiene Audio Setup, selección de skin, versión instalada y comprobación manual o automática de actualizaciones.

La colección Astra sustituye los diseños anteriores: **Astra / Obsidian**, **Tribal / Etched Titanium**, **Skulls / Bone & Carbon**, **Hippie / Sunset Paisley**, **Graffiti / Electric Ink**, **Purple Velvet / Amethyst**, **Stainless Steel / Precision**, **Ripped Black Denim / Roadworn**, **Blue Denim / Indigo** y **Spiderwebs / Black Widow**. Todas mantienen la misma geometría: rack, cabezal y cabina tienen el mismo ancho, con separación y apoyos propios. Seleccionar una previsualiza el cambio; solo queda aplicada al pulsar **APPLY SKIN**. Cerrar sin aplicar recupera la skin anterior. El VST3 utiliza exclusivamente Astra / Obsidian.

**CHECK FOR UPDATES** compara la versión instalada con la última release pública. La comprobación al iniciar puede activarse o desactivarse. Solo informa y nunca sustituye archivos, modelos o presets sin que el usuario abra la página de descarga.

## 14. Estado y ubicaciones

La aplicación restaura el NAM, IR, valores, skin, dispositivo y ruteo utilizados. Las carpetas portables con escritura guardan el estado junto al ejecutable. Los bundles de macOS y AppImage de Linux en modo lectura usan la carpeta de datos de usuario `Bcho/BchoNAMPlayer`.

Conserva los dos archivos de demostración en `Models` si quieres mantenerlos disponibles. Las IR del usuario no forman parte del paquete distribuido.

## 15. Solución de problemas

- **No hay sonido**: revisa POWER, ruta MAIN, interfaz y canales activos, INPUT VU, modelo y buffer.
- **Un bloque NAM no se activa**: carga un NAM válido en ese bloque y espera a que termine; una selección correcta lo activa automáticamente.
- **IR permanece en bypass**: carga una IR válida y comprueba que no hayas pulsado una segunda vez el elemento seleccionado.
- **Clics o cortes mientras tocas**: aumenta el buffer, usa ASIO oficial en Windows y evita buffers demasiado pequeños.
- **La carpeta NAM o IR aparece vacía**: comprueba que contiene directamente `.nam` o respuestas `.wav` cortas y válidas.
- **El nivel no coincide con otro reproductor NAM**: verifica la referencia 0 dBFS de la interfaz y el estado de Input Cali.
- **macOS impide el primer inicio**: haz clic derecho, elige **Abrir** y autoriza la aplicación no notarizada.
- **El AppImage no arranca**: concede permiso de ejecución y comprueba que el sistema dispone de audio x86_64 compatible.

## 16. Integridad y licencias

Compara los hashes de los ZIP con `SHA256SUMS.txt`. Bcho NAM Player incluye JUCE y Neural Amp Modeler Core; sus avisos están en `THIRD_PARTY_NOTICES.md`. La aplicación no concede derechos sobre capturas NAM o IR de terceros. Respeta la licencia incluida con cada archivo.
