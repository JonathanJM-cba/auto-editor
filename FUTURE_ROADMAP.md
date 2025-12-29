# Hoja de Ruta y Futuras Mejoras (Roadmap)

Este documento describe las funcionalidades avanzadas y expansiones propuestas para **Auto-Editor**. A diferencia de las mejoras arquitectónicas (GUIs, integraciones), estas sugerencias se centran en el **núcleo funcional** y la **inteligencia** de la herramienta.

## 1. Inteligencia Artificial Avanzada (Más allá del Silencio)

Actualmente, el proyecto destaca por editar basado en volumen y movimiento. El siguiente paso lógico es la **edición semántica**.

*   **Integración con LLMs (Modelos de Lenguaje)**:
    *   *Idea*: Usar la transcripción de Whisper para analizar el *contenido* del texto.
    *   *Feature*: "Cortar partes aburridas" o "Resumir video". Un LLM podría leer la transcripción y marcar timestamps de secciones redundantes o irrelevantes, indicándole a Auto-Editor que las corte.
*   **Edición Basada en Emociones**:
    *   *Idea*: Analizar la entonación y las expresiones faciales.
    *   *Feature*: Crear un "Highlight Reel" (resumen de mejores momentos) detectando risas, gritos de emoción o picos de actividad visual, ideal para gameplays o vlogs.
*   **Reencuadre Inteligente (Smart Crop)**:
    *   *Idea*: Convertir videos horizontales (16:9) a verticales (9:16) para TikTok/Shorts.
    *   *Feature*: Detectar automáticamente dónde está el sujeto hablante y mover el encuadre frame a frame para mantenerlo centrado.

## 2. Mejoras en Flujos de Trabajo (Workflow)

Facilitar casos de uso específicos que hoy requieren configuración manual compleja.

*   **Modo "Podcast Multicámara" Inteligente**:
    *   *Situación*: Tienes 3 archivos de video (Cámara A, Cámara B, Plano General) y 3 micrófonos.
    *   *Mejora*: Auto-Editor podría sincronizar los audios automáticamente y cambiar de cámara (corte multicam) enfocando a la persona que está hablando en ese momento, simulando un realizador de TV en vivo.
*   **Gestión Avanzada de Subtítulos**:
    *   *Mejora*: Generar estilos de subtítulos dinámicos ("Karaoke style" o palabra por palabra con animaciones) directamente en el renderizado, similar a lo que hacen apps como CapCut, pero automatizado por código.

## 3. Integración en la Nube y Redes

*   **Directo a YouTube/Cloud**:
    *   *Feature*: Módulos de autenticación (OAuth) para que, al terminar el renderizado, el video se suba automáticamente a un canal de YouTube (como privado) o a una carpeta de Google Drive/Dropbox, enviando una notificación al usuario.
*   **Soporte para Streaming (Experimental)**:
    *   *Feature*: Analizar un flujo RTMP en tiempo real para añadir metadatos de "corte sugerido" que luego puedan ser usados por OBS o reproductores personalizados para saltar silencios en vivo (con un ligero delay).

## 4. Expansión de Plataformas

*   **Versión Móvil (Core)**:
    *   *Desafío*: Portar la lógica a iOS/Android.
    *   *Estrategia*: Dado que Nim compila a C, se puede crear una librería compartida (`.so` / `.dylib`) que sea consumida por una app nativa en Swift o Kotlin, permitiendo editar videos grabados con el móvil directamente en el dispositivo sin subirlos a la nube.
*   **Plugins de Efectos de Sonido (VST)**:
    *   *Feature*: Permitir cargar plugins VST básicos para procesar el audio (compresión, ecualización, reducción de ruido) *antes* del análisis, mejorando la precisión de los cortes en entornos ruidosos.

## 5. Comunidad y Ecosistema

*   **Marketplace de "Recetas" (Presets)**:
    *   *Idea*: Un repositorio donde los usuarios compartan sus configuraciones de Auto-Editor (ej: "Configuración para Gameplay de Minecraft", "Configuración para Entrevista Formal").
    *   *Implementación*: Archivos YAML/JSON importables que configuran todos los umbrales y reglas de edición.

---
*Este roadmap sirve como guía para contribuidores que busquen desafíos de alto impacto para el proyecto.*
