# Compilación y Ejecución en Windows 11

Este documento detalla los pasos necesarios para compilar y ejecutar **Auto-Editor** desde el código fuente en Windows 11 utilizando el entorno **MSYS2**.

## 1. Requisitos Previos

### Nim
- Instala Nim usando [choosenim](https://github.com/dom96/choosenim#choosenim).
- Una vez instalado, asegúrate de tener la versión 2.x:
  ```bash
  nim --version
  ```

### MSYS2 (Toolchain de Compilación)
1. Descarga e instala [MSYS2](https://www.msys2.org/).
2. Abre la terminal **MSYS2 MINGW64**.
3. Instala todas las herramientas de compilación necesarias:
   ```bash
   pacman -S git make mingw-w64-x86_64-cmake mingw-w64-x86_64-meson mingw-w64-x86_64-ninja mingw-w64-x86_64-pkg-config mingw-w64-x86_64-yasm mingw-w64-x86_64-nasm patch
   ```

## 2. Configuración del Entorno

En la terminal **MSYS2 MINGW64**, asegúrate de que el binario de Nim esté en tu PATH (ajusta la ruta según tu usuario):
```bash
export PATH=$PATH:/c/Users/TU_USUARIO/.nimble/bin
```

## 3. Compilación

El proceso de compilación consta de dos fases:

### Fase A: Compilar Dependencias (FFmpeg + Librerías)
Esta tarea descarga y compila estáticamente todas las librerías necesarias (dav1d, x264, x265, whisper, etc.). **Puede tardar entre 20 y 40 minutos.**

```bash
nimble makeff
```

### Fase B: Compilar Auto-Editor
Una vez terminada la fase anterior, compila el ejecutable principal:

```bash
nimble make
```

## 4. Ejecución

Tras una compilación exitosa, se generará el archivo `auto-editor.exe` en la raíz del proyecto.

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

- **Error de permisos (Permission Denied)**: Si ocurre al mover carpetas, asegúrate de no tener archivos abiertos en el explorador o en otro programa que bloquee la carpeta `build`.
- **Rutas de archivos**: Utiliza siempre la terminal **MSYS2 MINGW64** para ejecutar comandos `nimble` para asegurar la compatibilidad de las librerías de sistema.
- **LTO Error**: Si el compilador falla en el paso final (Linking), el script está configurado para desactivar LTO automáticamente en Windows para mayor estabilidad.
