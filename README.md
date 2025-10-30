# DJ Controller - Pure Data Project

## 👥 Autores
- **Juan David Troncoso**
- **David Felipe Hurtado**

## 📋 Descripción

Este proyecto es un controlador de DJ profesional desarrollado en Pure Data (PD) que permite mezclar audio en tiempo real con dos decks independientes. El sistema incluye efectos de audio avanzados, sincronización entre decks y control completo sobre la mezcla.

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

**Fecha de Creación**: 2025  
**Versión**: 1.0  
**Plataforma**: Pure Data  
