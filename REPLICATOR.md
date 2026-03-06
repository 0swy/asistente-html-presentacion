# PROMPT DE RECONSTRUCCIÓN AUTOMÁTICA (REPLICATOR)

> **Rol:** Actúa como un Desarrollador Full-Stack experto en React y Web Speech API.
> **Misión:** Reconstruir el archivo fuente idéntico al original basado en las especificaciones lógicas detalladas a continuación.

## 1. Contexto del Software
- **Nombre:** THE SHARK'S SECRET - Interactive Presentation Coach.
- **Formato:** Archivo único HTML autónomo.
- **Stack:** React 18 (CDN), Babel, CSS3 (Variables), Web Speech API.

## 2. Especificaciones Técnicas Críticas

### A. Lógica de Reconocimiento de Voz "Blindada"
- **Continuidad:** `recognition.continuous = true` e `interimResults = true`.
- **Auto-reinicio:** Implementar lógica en `onend` para que, si `isListening` es true, el motor se reinicie tras 100ms.
- **Offset de Resultados (`resultOffsetRef`):** Para evitar que el texto de oraciones anteriores se repita en la nueva, usa un índice de referencia que se actualice al completar cada ítem.
- **Idempotencia:** En `onresult`, deriva el texto acumulado del ítem actual procesando únicamente desde el `resultOffsetRef`.

### B. Segmentación y Captura Atómica
- **Captura Segura:** Al marcar un ítem (Click o Barra Espaciadora), captura el valor de la voz en una constante local *antes* de resetear los buffers.
- **Estructura de Datos:** Almacena los segmentos en `fullTranscript` con el esquema: `[TITLE] {titulo} [TEXT] {texto} [SEP]`.

### C. Interfaz y Experiencia (UI/UX)
- **Modo Oscuro:** Fondo `#121212`, tarjetas `#1e1e1e`, acento amarillo `#ffd43b`.
- **Animaciones:** Los ítems completados deben usar `translateX(100px)` and `opacity: 0` con una transición de 400ms.
- **Auto-scroll:** El ítem con el foco actual (`highlightId`) debe mantenerse siempre visible mediante `scrollIntoView`.

## 3. Requisitos de Funcionalidad
- **Selector de Idiomas:** Menú desplegable para cambiar entre `en-US`, `es-ES` y `es-MX`.
- **Historial Lateral:** Panel `fixed` a la derecha con contador de ítems completados.
- **Resumen de Sesión:** Al detener el monitor, parsear los tags `[TITLE]` y `[TEXT]` para mostrar el desglose de lo dicho en cada oración.

---

## 4. Instrucción Final para la IA (The Prompt)
"Genera el código fuente completo de una aplicación React en un solo archivo HTML que cumpla con todos los puntos anteriores. Asegúrate de incluir la estructura de datos `CHECKLIST_DATA` con categorías de presentación (Hook, Problem, Solution, Science, Business, Closing). No omitas la lógica de prevención de duplicados ni el sistema de captura segura en `toggleId`."
