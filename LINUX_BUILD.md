# Compilación y Ejecución en Linux (Ubuntu / Debian)

Este documento detalla los pasos necesarios para compilar y ejecutar **Auto-Editor** desde el código fuente en distribuciones basadas en Debian, como Ubuntu.

## 1. Requisitos Previos

### Nim
Se recomienda instalar Nim usando **choosenim**:
```bash
curl https://nim-lang.org/choosenim/init.sh -sSf | sh
```
Asegúrate de que la versión instalada sea 2.2.2 o superior:
```bash
nim --version
```

### Dependencias del Sistema
Instala las herramientas de compilación y librerías necesarias:
```bash
sudo apt update
sudo apt install build-essential git make cmake meson ninja-build pkg-config \
    yasm nasm patch curl python3-pip libtool
```

## 2. Configuración del Entorno (Opcional)
Para que el comando `nim` sea reconocido permanentemente, cargá el PATH:
```bash
export PATH=$HOME/.nimble/bin:$PATH
```
(Podés agregar esta línea al final de tu `~/.bashrc` si querés que sea automático).

## 3. Compilación

El proceso de compilación consta de dos fases:

### Fase A: Compilar Dependencias (FFmpeg + Librerías)
Esta tarea descarga y compila estáticamente todas las librerías necesarias (dav1d, x264, x265, whisper, etc.) dentro de la carpeta del proyecto. **Puede tardar entre 20 y 40 minutos.**

```bash
nimble makeff
```

### Fase B: Compilar Auto-Editor
Una vez terminada la fase anterior, compila el binario principal:

```bash
nimble make
```

## 4. Ejecución

Tras una compilación exitosa, se generará el archivo `auto-editor` en la raíz del proyecto.

### Verificar versión
```bash
./auto-editor --version
```

### Ejemplo de uso
Para editar un video eliminando los silencios automáticamente:
```bash
./auto-editor video.mp4 --margin 0.1sec
```

## 5. Solución de Problemas Comunes

- **Permisos**: Asegúrate de tener permisos de escritura en la carpeta del proyecto. No se recomienda compilar como `root` a menos que sea necesario.
- **Memoria RAM**: La compilación de `x265`, `whisper` y el linkeo final pueden consumir bastante memoria. Se recomienda tener al menos 8GB de RAM.
- **LTO (Link Time Optimization)**: En sistemas Linux, LTO está desactivado por defecto en `ae.nimble` para acelerar la compilación y reducir el consumo de memoria en Máquinas Virtuales. Si deseas habilitarlo para obtener un binario levemente más optimizado, puedes editar `ae.nimble`.
- **Whisper (Transcripción)**: Si la compilación de whisper falla, puedes intentar deshabilitarla temporalmente configurando la variable de entorno: `export DISABLE_WHISPER=1` antes de correr `nimble makeff`.
