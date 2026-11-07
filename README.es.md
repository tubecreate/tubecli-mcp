<p align="center">
  <img src="https://cloud.tubecreate.com/logo.svg" width="96" alt="Logo de TubeCLI">
</p>

<h1 align="center">TubeCLI MCP Connector</h1>

<p align="center">
  Conecta Claude, Gemini, Grok, Muse AI y otras apps de IA a tus servidores TubeCLI a través de <b>cloud.tubecreate.com</b>.
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <b>Español</b> ·
  <a href="README.ja.md">日本語</a> ·
  <a href="README.ko.md">한국어</a> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.tr.md">Türkçe</a> ·
  <a href="README.zh-CN.md">简体中文</a> ·
  <a href="README.zh-TW.md">繁體中文</a>
</p>

---

## ¿Qué es TubeCLI?

TubeCLI es un sistema de automatización que instalas y ejecutas tú mismo, pensado para **crear videos automáticamente de principio a fin**:

1. **Guion.** La IA investiga el tema y escribe el guion.
2. **Voz.** El guion se lee en voz alta con voces de IA.
3. **Imágenes y video.** Cada escena se ilustra con imágenes de IA y clips cortos de video generados con IA, por ejemplo con Muse AI.
4. **Edición.** Se añaden subtítulos, diseño y música, y se exporta el video final.
5. **Miniatura y SEO.** Se generan y revisan la miniatura, el título, la descripción y las etiquetas.
6. **Publicación.** El video se sube a YouTube y a otras plataformas, con fecha y hora programadas si lo deseas.

TubeCLI funciona en tu propia computadora o VPS. Además controla perfiles de navegador reales, ejecuta agentes de IA
según un horario y gestiona un tablero de tareas. **TubeCLI Cloud** (`cloud.tubecreate.com`) es el panel que reúne
todos tus servidores en un solo lugar.

El **Conector MCP** permite que una app de IA se comunique con tus servidores a través de TubeCLI Cloud. Puedes pedirle
a Claude o a Gemini que cree una tarea de video, que revise qué está haciendo un agente, que lea una página en un perfil
de navegador o que comparta un video terminado.

## La URL del conector

```
https://cloud.tubecreate.com/mcp
```

Es un servidor MCP remoto (Streamable HTTP) con inicio de sesión OAuth 2.1. Las apps compatibles se registran solas,
así que normalmente solo tienes que pegar la URL. No hay ninguna clave de API que copiar.

## Antes de empezar

- Una **cuenta de TubeCLI Cloud** en [cloud.tubecreate.com](https://cloud.tubecreate.com).
- Al menos un **servidor TubeCLI** añadido a esa cuenta: tu propia computadora (*Connect my computer*) o un VPS.
  Debes ser su propietario, o el servidor debe estar compartido contigo como **administrador**.
- El servidor debe tener **TubeCLI 2026.08.09.217 o una versión más reciente**. Si un servidor está desactualizado,
  el panel muestra un botón para actualizarlo.

## Conecta tu app de IA

Todas las apps terminan en la misma página de inicio de sesión de TubeCLI. Ahí eliges **qué servidores** puede usar la
app y el **nivel de acceso** (*Solo lectura* o *Leer y cambiar*), y luego pulsas **Permitir**.

### Claude (claude.ai, Claude Desktop)

1. Abre **Settings › Connectors** (en claude.ai: **Customize › Connectors**).
2. Elige **Add custom connector**.
3. Ponle de nombre `TubeCLI` y pega `https://cloud.tubecreate.com/mcp`.
4. Pulsa **Connect**, inicia sesión en TubeCLI Cloud, elige los servidores y pulsa **Permitir**.

### Claude Code

```bash
claude mcp add --transport http tubecli https://cloud.tubecreate.com/mcp
```

Después ejecuta `/mcp` dentro de Claude Code y elige **tubecli** para iniciar sesión.

### Gemini

1. Abre [gemini.google.com › Connectors](https://gemini.google.com/customize/connectors) y pulsa **+ Custom**.
2. Pega `https://cloud.tubecreate.com/mcp` en **MCP Server URL**.
3. Deja vacíos **Client ID** y **Client secret** y pulsa **Next**.
4. Inicia sesión en TubeCLI Cloud, elige los servidores y pulsa **Permitir**.

Si Gemini sigue mostrando un error anterior, pulsa **Cancel** y vuelve a abrir **+ Custom**.

### Muse AI ([muse.ai](https://muse.ai), Meta)

1. En Muse AI, añade un conector personalizado con la URL `https://cloud.tubecreate.com/mcp`.
2. Pulsa **Connect**, inicia sesión en TubeCLI Cloud, elige los servidores y pulsa **Permitir**.

Si Muse AI muestra *Missing required parameters* (faltan parámetros obligatorios), elimina el conector y vuelve a añadirlo.
A veces Muse AI reutiliza una sesión antigua.

### Grok

Añade un conector personalizado (servidor MCP remoto) en Grok con la URL `https://cloud.tubecreate.com/mcp`, luego
inicia sesión y pulsa **Permitir**.

### Otros clientes MCP

Cualquier cliente que admita servidores MCP remotos con OAuth 2.1 (PKCE y registro dinámico de clientes) puede conectarse.
Si tu app te pide un Client ID, crea uno en **TubeCLI Cloud › Conector MCP**, en la sección
*Apps que piden un Client ID (Gemini)*: pega la redirect URI que muestra la app y luego copia el Client ID y el
Client Secret de vuelta en la app. El secreto se muestra una sola vez.

## Qué puede hacer la app de IA

| Área | Herramientas |
|---|---|
| Servidores y ayuda | `servers_list`, `tubecli_overview`, `tubecli_doc`, `tubecli_endpoints` |
| Cualquier función de TubeCLI (tareas de video, agentes, Content Studio, programaciones…) | `tubecli_api` |
| Tablero de tareas | `board_list`, `board_task`, `board_create` |
| Perfiles de navegador (tus sesiones ya iniciadas) | `browser_profiles`, `browser_open`, `browser_goto`, `browser_read`, `browser_click`, `browser_type`, `browser_scroll`, `browser_screenshot`, `browser_nav`, `browser_close` |
| Mercado y configuración de servidores | `market_install`, `server_clone`, `clone_manifest`, `clone_export`, `clone_import`, `clone_status` |
| Enlaces públicos para compartir resultados | `share_find`, `share_file`, `share_files`, `share_list`, `share_revoke` |
| Agent Town | `town_agent_offer` |
| Aprobaciones | `approval_result` |

### Ejemplos de peticiones

- *"Muestra mis servidores TubeCLI y dime qué tareas de video se están ejecutando."*
- *"Crea un video en inglés de 6 minutos sobre la historia del café, con miniatura, y prográmalo en YouTube para mañana a las 9 a. m."*
- *"¿Por qué falló la última tarea de video? Vuelve a intentarlo."*
- *"Busca los videos que se terminaron ayer y dame enlaces para compartirlos."*
- *"Abre mi perfil de YouTube en el navegador y lee los comentarios del video más reciente."*

## Seguridad y control

- **Tú eliges los servidores.** La app solo llega a los servidores que te pertenecen o que administras y que elegiste
  al conectarla. Los colaboradores no pueden conectar una app a un servidor compartido.
- **Dos niveles de acceso.** *Solo lectura* puede ver, pero no cambiar nada. *Leer y cambiar* también puede hacer cambios habituales.
- **Aprobación para acciones delicadas.** Borrar o cancelar, detener un navegador, instalar extensiones y publicar en
  Agent Town devuelven un enlace de aprobación. No se ejecuta nada hasta que lo abras y pulses **Aprobar y ejecutar**.
- **Fuera de alcance.** Las cuentas, las contraseñas, las claves de API y los archivos sin procesar quedan fuera del alcance de la app.
- **Los enlaces públicos son opcionales.** Marca *Permitir enlaces públicos para compartir* en una conexión para que la
  app pueda compartir imágenes y videos. Por defecto, los enlaces duran 30 minutos. Si desmarcas la casilla, se revocan.
- **Revoca el acceso cuando quieras.** **TubeCLI Cloud › Conector MCP** muestra cada conexión con su actividad reciente.
  *Desconectar* corta el acceso al instante. Cada servidor tiene además su propio interruptor de encendido y apagado.
- **Inicio de sesión estándar.** Se usa OAuth 2.1 con PKCE. Los tokens son opacos y se guardan solo como hash. Los
  tokens de acceso duran 1 hora y se renuevan solos.

## Solución de problemas

| Problema | Qué hacer |
|---|---|
| La app muestra `401` o *session expired* | Quita el conector en la app y vuelve a añadirlo. Comprueba que la conexión sigue apareciendo en **Conector MCP**. |
| *Couldn't register* / *redirect URL was rejected* | Asegúrate de haber pegado exactamente `https://cloud.tubecreate.com/mcp` y vuelve a intentarlo. Si sigue pasando, abre un issue con el nombre de la app y el texto del error. |
| Un servidor no aparece en la página de inicio de sesión | Debe estar en línea, tener TubeCLI 2026.08.09.217+, y tú debes ser su propietario o administrador. |
| Una herramienta dice que el conector está desactivado en un servidor | En **Conector MCP**, pulsa *Activar* junto a ese servidor. |
| Una acción devolvió un enlace de aprobación | Abre el enlace, revisa la acción y pulsa **Aprobar y ejecutar**; luego dile a la app que ya está aprobada. |

## Enlaces

- TubeCLI Cloud: [cloud.tubecreate.com](https://cloud.tubecreate.com)
- TubeCLI: [tubecli.app](https://tubecli.app) · [github.com/tubecreate/tubecli](https://github.com/tubecreate/tubecli)
- Model Context Protocol: [modelcontextprotocol.io](https://modelcontextprotocol.io)

¿Preguntas o problemas? [Abre un issue](https://github.com/tubecreate/tubecli-mcp/issues).
