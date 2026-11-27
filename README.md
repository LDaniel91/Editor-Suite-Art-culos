# Editorial Suite — Maquetar Artículos

Editorial Suite es una herramienta web en un solo archivo HTML para apoyar la maquetación y conversión de artículos científicos a formatos editoriales. Permite pegar un artículo fuente, usar una plantilla HTML de referencia y generar salidas en XML, HTML, PDF, EPUB, texto crudo y paquete ZIP.

El proyecto está pensado para trabajar desde el navegador, tanto en computadora de escritorio como en móvil, y puede publicarse en línea para usarse como aplicación web o como base de una app Android tipo WebView/WebToApp.

## Características principales

- Interfaz responsive para PC, tableta y móvil.
- Modo claro y modo oscuro con colores naranja, verde, blanco y negro.
- Entrada de artículo completo en texto, Markdown o documento Word cargado desde archivo.
- Plantilla HTML de referencia para adaptar la salida al estilo de una revista.
- Notas o esquema adicional para orientar la conversión.
- Selección de base de datos o revista destino.
- Generación de formatos:
  - XML editorial. En destinos JATS/SciELO, las tablas y figuras se referencian como imágenes (`graphic`) y el programa genera los archivos PNG correspondientes para el ZIP.
  - HTML maquetado.
  - PDF de texto derivado del HTML, con fondo blanco, estilos editoriales, texto seleccionable y enlaces clicables.
  - EPUB derivado del HTML.
  - Vista Raw.
  - Paquete ZIP con los archivos generados.
- Vista previa del HTML generado.
- Editor de prompts por destino y tipo de salida.
- Configuración de proveedor de IA, modelo, tokens y temperatura.
- Guardado local de la configuración en el navegador mediante `localStorage`.

## Uso rápido

1. Abre `index.html` en un navegador moderno.
2. Selecciona la base de datos o revista destino.
3. Marca los formatos que deseas generar.
4. Pega o carga el artículo fuente.
5. Si tienes una plantilla HTML de la revista, pégala o cárgala en el bloque correspondiente.
6. Añade notas adicionales si son necesarias.
7. Pulsa **Generar archivos**.
8. Revisa las pestañas XML, HTML, PDF, EPUB, Raw o Paquete. En la pestaña XML puedes alternar entre **Vista previa** (el artículo renderizado desde el XML) y **Código XML**.
9. Descarga el ZIP cuando el resultado esté listo.

## Configuración de IA

La aplicación incluye una ventana de configuración para seleccionar proveedor, modelo y clave API. La clave se guarda solo en el navegador del usuario mediante `localStorage`.

No subas claves API, contraseñas ni tokens al repositorio.

## Uso en línea

Para usar el proyecto en línea, publica el archivo `index.html` en un servicio de alojamiento estático, por ejemplo GitHub Pages, Cloudflare Pages, Netlify o Vercel.

Ejemplo con GitHub Pages:

1. Sube `index.html` a la raíz del repositorio.
2. Entra en **Settings → Pages**.
3. Selecciona la rama principal y la carpeta raíz.
4. Guarda los cambios.
5. Usa la URL generada para abrir la herramienta o conectarla a WebToApp.

## Uso con WebToApp

Para crear una app Android con WebToApp:

1. Publica primero el proyecto en una URL accesible.
2. En WebToApp crea la aplicación en modo **Website URL**.
3. Pega la URL pública del proyecto.
4. Activa JavaScript y almacenamiento DOM.
5. Genera el APK o AAB.

Cuando actualices `index.html` en el repositorio y se vuelva a publicar, la app cargará la versión nueva al abrirse.

## Estructura del repositorio

```text
.
├── index.html
└── README.md
```

## Dependencias cargadas por CDN

El archivo `index.html` carga estas librerías desde CDN:

- Mammoth, para leer documentos `.docx`.
- JSZip, para crear paquetes ZIP y EPUB.
- jsPDF 2.5.1, para generar el PDF de texto desde el HTML.

Por eso, para usar todas las funciones se recomienda conexión a Internet al abrir la herramienta.

## Privacidad y seguridad

- El contenido pegado por el usuario se procesa en el navegador y en el proveedor de IA configurado por el propio usuario.
- La clave API no debe compartirse ni guardarse en el repositorio.
- Revisa siempre el resultado generado antes de enviarlo a una revista o base de datos.
- Si el repositorio es privado, la página publicada puede seguir siendo accesible para quien tenga la URL, según el servicio de publicación usado.

## Estado del proyecto

Proyecto en desarrollo. La versión actual se centra en una interfaz única, responsive y con modo claro/oscuro para facilitar la maquetación de artículos científicos desde cualquier dispositivo.

## Uso sin saldo en USD

Si no puedes recargar una API de pago, usa el proveedor **Manual sin API (DeepSeek web)** en Configuración. El programa mostrará el prompt completo para copiarlo en DeepSeek web u otra IA gratuita; luego pegas la respuesta en la ventana manual y Editorial Suite continúa generando XML, HTML, PDF, EPUB y ZIP. La ventana manual cuenta los caracteres, indica la etiqueta de cierre esperada y no acepta respuestas incompletas: si la IA se corta, pega la continuación al final del mismo cuadro o carga la respuesta desde un archivo .txt, .md, .html o .xml. También puedes descargar el prompt como archivo de texto si el copiado se corta.

También se incluyen opciones gratuitas con límites, como **OpenRouter Free** y **Groq Free**, siempre que puedas registrarte y obtener una API Key sin pago. DeepSeek API requiere saldo prepagado; si devuelve error 402, significa saldo insuficiente.

