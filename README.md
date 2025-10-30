# DJ Controller - Pure Data Project

## 👥 Autores
- **Juan David Troncoso**
- **David Felipe Hurtado**

## 📋 Descripción

Este proyecto es un controlador de DJ profesional desarrollado en Pure Data (PD) que permite mezclar audio en tiempo real con dos decks independientes. El sistema incluye efectos de audio avanzados, sincronización entre decks y control completo sobre la mezcla.

### 🎥 Video Demostración

**[Ver video del proyecto en YouTube](https://youtu.be/MS1P-mApcHQ)**

[![Video Demo](https://img.shields.io/badge/YouTube-Ver%20Demo-red?style=for-the-badge&logo=youtube)](https://youtu.be/MS1P-mApcHQ)

## ✨ Características Principales

### 🎚️ Dual Deck System

El proyecto cuenta con dos decks independientes (Deck 1 y Deck 2) con las siguientes características:

#### Deck 1
- **Control de Volumen**: Ajuste de volumen de 0 a 1
- **Filtros de Audio**:
  - Filtro Low Pass (0-10000 Hz)
  - Filtro High Pass (0-10000 Hz)
- **Efectos**:
  - Reverb con control Wet/Dry (0-1)
  - Delay ajustable con control de mezcla (0-1)
- **Controles de Reproducción**:
  - Play/Stop independiente
  - Carga de archivos de audio (.wav, .aiff, etc.)
  - Visualización de samples cargados

#### Deck 2
- Mismas características que Deck 1
- Independiente para permitir mezcla profesional
- Sincronización opcional con Deck 1

### 🎛️ Efectos de Audio

- **Reverb**: Efecto de reverberación ajustable con control wet/dry
- **Delay**: Delay estéreo con tiempo de hasta 2000ms
- **Filtros**: High-pass y Low-pass configurables
- **Limitador**: Clip de seguridad (-0.99 a 0.99) para proteger el audio

### 🔄 Sincronización

- **SYNC_PLAY**: Botón verde para reproducir ambos decks simultáneamente
- **SYNC_STOP**: Botón rojo para detener ambos decks al mismo tiempo

### 🥁 Instrumentos de Percusión Integrados

El proyecto incluye sintetizadores integrados:

- **TR-808 Snare**: Emulación de caja de batería clásica con controles de:
  - Decay (50-2000ms)
  - Noise (100-10000)
  - Presets configurables

- **Cymbal**: Sintetizador de platillo con:
  - 6 osciladores de pulso
  - Filtros resonantes configurables
  - Control de frecuencia base (220Hz default)
  - Envelope de volumen y ruido

### 🎧 Control OSC

- **Puerto**: 5580 UDP
- **Protocolo**: OSC (Open Sound Control)
- Permite control remoto desde aplicaciones externas (TouchOSC, Max/MSP, etc.)

## 🔧 Requisitos

- **Pure Data** (versión 0.47 o superior)
- **Pure Data Extended** (recomendado para soporte completo de objetos)
- Sistema operativo: Windows, macOS o Linux
- Tarjeta de audio (recomendado para latencia baja)

## 🚀 Instalación y Uso

1. **Instalar Pure Data**:
   - Descarga Pure Data desde [puredata.info](https://puredata.info/)
   - Instala siguiendo las instrucciones de tu sistema operativo

2. **Abrir el Proyecto**:
   ```
   Abre Pure Data
   File > Open > Selecciona Project4.pd
   ```

3. **Configurar Audio**:
   - Ve a `Media > Audio Settings`
   - Configura tu interfaz de audio
   - Ajusta el buffer size (64 o 128 samples recomendado)

4. **Cargar Audio**:
   - Haz clic en los botones `CARGAR_D1` o `CARGAR_D2`
   - Selecciona archivos de audio (.wav, .aiff)
   - Los samples se cargarán en los arrays respectivos

5. **Reproducir**:
   - Usa los botones `PLAY_D1` / `PLAY_D2` para cada deck
   - O usa `SYNC_PLAY` para reproducir ambos simultáneamente
   - Ajusta volumen, filtros y efectos en tiempo real

## 🎮 Controles

### Parámetros Principales

| Control | Rango | Función |
|---------|-------|---------|
| VOLUMEN_DECK1/2 | 0-1 | Volumen principal del deck |
| FILTRO_LOW_D1/2 | 0-10000 | Frecuencia de corte del filtro paso bajo |
| FILTRO_HIGH_D1/2 | 0-10000 | Frecuencia de corte del filtro paso alto |
| REVERB_WET_D1 | 0-1 | Cantidad de señal con reverb |
| REVERB_DRY_D1 | 0-1 | Cantidad de señal directa |
| DELAY_MIX_D1 | 0-1 | Mezcla del efecto delay |

### Botones

- 🟢 **SYNC_PLAY**: Reproducir ambos decks sincronizados
- 🔴 **SYNC_STOP**: Detener ambos decks
- ▶️ **PLAY_D1/D2**: Reproducir deck individual
- ⏹️ **STOP_D1/D2**: Detener deck individual
- 📁 **CARGAR_D1/D2**: Cargar archivo de audio

## 🎵 Control OSC Remoto

El proyecto escucha en el puerto UDP 5580 y acepta mensajes OSC con el formato:

```
/1_fader1 <valor>
```

Puedes controlar el sistema remotamente usando aplicaciones como:
- **TouchOSC** (iOS/Android)
- **Max/MSP**
- **Processing**
- Cualquier cliente OSC

## 📊 Arquitectura del Audio

```
Audio Input → Array (deck1/deck2)
    ↓
Filters (hip~/lop~)
    ↓
Effects (freeverb~/delay)
    ↓
Volume Control
    ↓
Mixer (+~)
    ↓
Output (dac~)
```

## 🛠️ Personalización

### Modificar Presets de Percusión

Edita los mensajes en el patch para cambiar los presets del TR-808 Snare:
```
; tr808sn_decay 200
; tr808sn_noise 300
```

### Ajustar Tiempo de Delay

Modifica los objetos `delwrite~` y `delread~`:
```
delwrite~ delayL1 <tiempo_en_ms>
```

## 📝 Notas Técnicas

- **Sample Rate**: Depende de la configuración de Pure Data (típicamente 44100 Hz)
- **Buffer Size**: Ajustable en configuración de audio
- **Latencia**: Menor buffer = menor latencia (pero mayor uso de CPU)
- **Formato de Audio**: Compatible con WAV, AIFF y formatos soportados por `soundfiler`

## 🐛 Solución de Problemas

### No se escucha audio
- Verifica que DSP esté activado (casilla "Compute Audio" marcada)
- Revisa la configuración de audio en Media > Audio Settings
- Asegúrate de que los archivos estén cargados correctamente

### Latencia alta
- Reduce el buffer size en la configuración de audio
- Usa una interfaz de audio profesional
- Cierra otras aplicaciones que usen audio

### Mensajes OSC no funcionan
- Verifica que el puerto 5580 no esté siendo usado por otra aplicación
- Asegúrate de que el mensaje `listen 5580` esté enviado (automático con loadbang)
- Revisa el formato de tus mensajes OSC

## 📚 Recursos Adicionales

- [Pure Data Documentation](https://puredata.info/docs)
- [OSC Protocol Specification](http://opensoundcontrol.org/)
- [Pure Data Tutorials](https://puredata.info/docs/tutorials)

## 📄 Licencia

Este proyecto fue desarrollado con fines educativos para la Universidad.

## 🙏 Agradecimientos

Proyecto desarrollado como parte del curso de procesamiento de audio digital.

---

## 🎬 Guion de Video — Proyecto Pure Data + Clean OSC + TR-808

### 🎤 [0:00 – 0:20] Introducción

"Hola, mi nombre es David Hurtado, y hoy voy a mostrar mi proyecto hecho en Pure Data.
Este patch combina control remoto desde mi celular con Clean OSC y síntesis de sonido tipo TR-808.

Con la app controlo cosas como volumen, filtros, reverb, delay y sincronización, y además tengo percusión generada directamente en Pure Data."

*(Muestra el patch completo y luego la app Clean OSC en tu celular.)*

---

### 🎤 [0:20 – 1:00] Conexión OSC (parte superior izquierda del patch)

"Primero está la parte de comunicación OSC, que conecta Pure Data con mi celular.

El objeto `[netreceive -u -b 5580]` recibe los mensajes que vienen por el puerto 5580.
Luego, `[oscparse]` interpreta esos datos, y `[list trim]` limpia la información.

Finalmente, con `[route]`, separo los mensajes según su nombre:
volumen1, filtrobass1, filtrohigh1, reverb1, delay1, volumen2, filtrobass2, filtrohigh2, sync y syncstop."

*(Mueve un control en Clean OSC y muestra cómo cambia un valor o aparece en la consola de PD.)*

"Por ejemplo, si muevo el volumen 1 en mi celular, se modifica el control de volumen del Deck 1 en tiempo real."

---

### 🎤 [1:00 – 2:00] Deck 1 — Cargar, reproducir y procesar audio

"Aquí tengo el Deck 1, que actúa como un reproductor de audio.

Con el botón CARGAR_D1, abro una ventana con `[openpanel]` y selecciono un archivo.
Ese archivo se carga en un arreglo llamado deck1 con `[soundfiler]`."

*(Haz clic en CARGAR_D1 y muestra cómo cargas un audio.)*

"El botón PLAY_D1 envía el mensaje '1' para que `[tabplay~ deck1]` empiece la reproducción.
El botón STOP_D1 envía 'stop' para detenerla."

*(Presiona los botones PLAY y STOP.)*

"Luego aplico filtros:
- `[hip~ 20]` elimina frecuencias muy graves
- `[lop~ 10000]` corta las más altas

El filtro de bajos y altos también puede modificarse desde el celular usando Clean OSC.

Después el audio pasa por control de volumen, un limitador `[clip~ -0.99 0.99]`, una reverb con `[freeverb~]`, y un delay controlado por el parámetro Delay1 de la app."

---

### 🎤 [2:00 – 2:40] Deck 2 — Segundo reproductor

"El Deck 2 funciona igual que el primero.

Puedo cargar otra pista con CARGAR_D2, reproducir o detenerla con PLAY_D2 y STOP_D2, y controlar sus filtros y volumen con los deslizadores de la app.

Ambos decks se mezclan con `[+~]` y se envían al objeto `[dac~]`, que representa la salida de audio del computador."

*(Muestra cómo subes y bajas los volúmenes de ambos decks desde el celular.)*

---

### 🎤 [2:40 – 3:10] Sincronización

"Con los botones Sync y Syncstop de Clean OSC puedo reproducir o detener los dos decks al mismo tiempo.

En Pure Data, esos botones activan los objetos SYNC_PLAY y SYNC_STOP, que envían señales a ambos reproductores a la vez."

*(Presiona los botones desde la app para demostrarlo.)*

---

### 🎤 [3:10 – 4:10] TR-808 Snare y Cymbal — Percusión sintética

"También añadí una sección de percusión inspirada en la Roland TR-808.

En el subpatch `pd tr808-snare`, tengo un generador de snare o redoblante que usa ruido blanco (`[noise~]`) y filtros `[vcf~]` para simular el golpe clásico de la 808.

Este sonido se dispara con un bang, y puedo ajustar parámetros como pitch, decay y mezcla de ruido usando los deslizadores que creé.

Luego, en el subpatch `pd cymbal`, genero un platillo (hi-hat o crash) usando varios osciladores `[phasor~]` combinados con ruido y filtros.

Así tengo percusión 100% sintética, sin usar samples."

*(Presiona los bangs para escuchar el snare y el cymbal, mostrando cómo cambian los sliders.)*

---

### 🎤 [4:10 – 4:40] Mezcla final

"Todos los sonidos —los dos decks, la reverb, el delay y la percusión— se mezclan antes de llegar a `[dac~]`, la salida de audio.

Esto me permite tener un pequeño sistema de mezcla digital, controlado completamente desde el celular con Clean OSC."

---

### 🎤 [4:40 – 5:00] Cierre

"En resumen, este proyecto combina control OSC, reproducción de audio, efectos y síntesis de percusión tipo TR-808, todo dentro de Pure Data.

Es una forma práctica de aprender sobre procesamiento de audio, control remoto y síntesis digital.

Gracias por ver el video."

---

**Fecha de Creación**: 2025  
**Versión**: 1.0  
**Plataforma**: Pure Data  
