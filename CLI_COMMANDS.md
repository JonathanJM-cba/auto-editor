# Comandos Básicos de Auto-Editor (CLI)

Este documento presenta los comandos más comunes para utilizar **Auto-Editor** desde la línea de comandos una vez compilado.

## 1. Uso Básico

El uso más simple elimina los silencios de un video usando los valores por defecto:
```bash
./auto-editor video.mp4
```
Esto generará un archivo llamado `video_ALTERED.mp4`.

## 2. Ajuste de Márgenes

Para evitar que los cortes suenen muy abruptos, podés agregar un margen de tiempo antes y después de cada sección ruidosa:
```bash
./auto-editor video.mp4 --margin 0.1sec
```
*También podés usar unidades como `0.1s`, `2f` (2 frames), etc.*

## 3. Cambiar Velocidades

Podés elegir a qué velocidad se reproducen las partes "silenciosas" y las partes "normales":

- **Eliminar silencios por completo (por defecto):**
  ```bash
  ./auto-editor video.mp4 --silent-speed 99999
  ```
- **Cámara rápida en silencios (ej. 10x):**
  ```bash
  ./auto-editor video.mp4 --silent-speed 10
  ```
- **Cámara lenta en las partes con sonido (ej. 0.5x):**
  ```bash
  ./auto-editor video.mp4 --video-speed 0.5
  ```

## 4. Edición basada en Transcripción (Whisper)

Si compilaste con soporte para Whisper, podés editar basándote en la voz en lugar de solo el volumen:
```bash
./auto-editor video.mp4 --edit audio:threshold=0.1
```
O usar comandos específicos de whisper para ver la transcripción:
```bash
./auto-editor whisper video.mp4
```

## 5. Exportar a otros formatos

Si preferís terminar la edición en un programa profesional, podés exportar un archivo de proyecto:

- **Para Adobe Premiere Pro:**
  ```bash
  ./auto-editor video.mp4 --export premiere
  ```
- **Para DaVinci Resolve:**
  ```bash
  ./auto-editor video.mp4 --export resolve
  ```
- **Para Final Cut Pro:**
  ```bash
  ./auto-editor video.mp4 --export final-cut-pro
  ```

## 6. Ver Estadísticas (Sin Renderizar)

Si solo querés ver cuánto tiempo se ahorraría sin generar el video final, usá `--preview`:
```bash
./auto-editor video.mp4 --preview
```

## 7. Ayuda Completa

Para ver todas las opciones disponibles (que son muchísimas):
```bash
./auto-editor --help
```
