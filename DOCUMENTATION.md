# Documentación del Proyecto Auto-Editor

## Introducción
**Auto-Editor** es una aplicación de línea de comandos diseñada para automatizar la edición de video y audio. Su función principal es analizar el contenido multimedia (por ejemplo, detectando el volumen del audio) para realizar cortes automáticos, eliminando las partes silenciosas o "espacios muertos". Esto crea un primer borrador del video ("first pass") de manera rápida, ahorrando tiempo en tareas repetitivas de edición.

El proyecto ha sido reescrito y optimizado utilizando el lenguaje de programación **Nim**, lo que le otorga un alto rendimiento y eficiencia.

## Tecnologías Utilizadas

Este proyecto utiliza una combinación de tecnologías modernas para el procesamiento multimedia de alto rendimiento:

*   **Lenguaje Principal**: 
    *   **Nim** (versión >= 2.2.2): Elegido por su eficiencia cercana a C/C++ y su sintaxis expresiva.
*   **Procesamiento Multimedia**:
    *   **FFmpeg**: El motor núcleo para leer, manipular y escribir archivos de video y audio. El proyecto incluye scripts para compilar una versión estática y personalizada de FFmpeg con codecs específicos.
*   **Codecs y Librerías de Apoyo** (gestionados en el proceso de compilación):
    *   **x264 / x265**: Para codificación de video H.264 y HEVC.
    *   **libvpx/dav1d/SVT-AV1**: Para codecs VP9 y AV1.
    *   **LAME/Opus**: Para codificación de audio.
    *   **Whisper.cpp**: Integración para edición basada en reconocimiento de voz (transcripción).
*   **Herramientas de Construcción (Build System)**:
    *   **Nimble**: El gestor de paquetes y sistema de construcción de Nim.
    *   **Meson, Ninja, CMake**: Utilizados para compilar las dependencias de bajo nivel (como las librerías de video).

## Requisitos Previos

Para compilar este proyecto desde el código fuente, necesitarás tener instalado en tu sistema:

1.  **Nim**: El compilador de Nim y su gestor de paquetes `nimble`.
2.  **Compilador de C**: Como `gcc` o `clang`.
3.  **Herramientas de Build**: `cmake`, `meson`, `ninja`, `git`, `yasm` o `nasm` (para ensamblador).
4.  **Python** (opcional, pero puede requerirse para algunos scripts de ayuda o instalación de `meson` si no está en el sistema).

## Paso a Paso: Compilación

El proceso de compilación consta de dos fases principales: preparar las dependencias (ffmpeg personalizado) y compilar la aplicación en sí.

### 1. Preparar Dependencias (FFmpeg)
El archivo `ae.nimble` contiene una tarea específica para descargar y compilar FFmpeg y sus dependencias de forma estática.

Ejecuta el siguiente comando en la raíz del proyecto:

```bash
nimble makeff
```
*Este paso puede tardar varios minutos ya que descarga y compila múltiples librerías.*

### 2. Compilar Auto-Editor
Una vez que las dependencias están listas, compila el binario principal de la aplicación:

```bash
nimble make
```

Esto generará un archivo ejecutable `auto-editor` (o `auto-editor.exe` en Windows) en la carpeta raíz.

### Notas para Windows
Si estás en Windows, el proyecto sugiere el uso de entornos tipo Unix (como MSYS2 o Git Bash con MinGW) o la compilación cruzada si se define en las tareas. Sin embargo, para una ejecución nativa, asegúrate de tener las herramientas en tu PATH. El archivo `ae.nimble` tiene una tarea `makeffwin` diseñada para compilación cruzada hacia Windows, lo cual sugiere que compilar nativamente en Windows puede requerir configuración extra de MinGW.

## Ejecución y Uso (CLI)

Una vez compilado, puedes usar el ejecutable directamente desde la línea de comandos.

### Comando Básico
El uso más simple es pasarle un archivo de video. Auto-Editor analizará el audio y cortará las partes silenciosas usando la configuración por defecto.

```bash
# Ejecutar desde la carpeta actual
./auto-editor video_ejemplo.mp4
```

### Ejemplo Paso a Paso

Supongamos que tienes un video llamado `entrevista.mp4` y quieres eliminar los silencios, pero dejando un pequeño margen para que los cortes no sean tan bruscos.

1.  **Abre tu terminal** en la carpeta donde compilaste el proyecto.
2.  **Ejecuta el comando** con la opción `--margin` (margen):
    ```bash
    ./auto-editor entrevista.mp4 --margin 0.2s
    ```
    *Esto dejará 0.2 segundos de "aire" antes y después de cada corte.*

3.  **Verifica el resultado**: El programa generará un nuevo archivo (por defecto añade `_ALTERED` al nombre o similar, o exporta un XML si se pide) con los cortes aplicados.

### Otras Opciones Comunes

*   **Exportar para Editores Profesionales**:
    Si prefieres no renderizar un video nuevo, sino importar los cortes en Adobe Premiere, DaVinci Resolve, etc.
    ```bash
    ./auto-editor entrevista.mp4 --export premiere
    ./auto-editor entrevista.mp4 --export resolve
    ```

*   **Editar basado en Movimiento** (en lugar de audio):
    ```bash
    ./auto-editor video_accion.mp4 --edit motion:threshold=0.02
    ```

Para ver todas las opciones disponibles:
```bash
./auto-editor --help
```
