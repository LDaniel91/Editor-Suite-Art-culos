# Editorial Suite · Multi-Formato v1.2

Herramienta de un solo archivo (`index.html`) que convierte un artículo científico (texto, Markdown o Word) en un paquete editorial: **XML** de metadatos/marcado para la base de datos elegida, **HTML5** semántico, **PDF**, **EPUB 3** y un **ZIP** con todo. Funciona en el navegador (PC y móvil) y se puede empaquetar como APK con WebToApp o similar.

La IA hace el marcado; el programa hace lo determinista: validar, generar tablas/figuras como imágenes, construir PDF/EPUB y empaquetar.

## Uso rápido
1. Elige la **base de datos destino** (SciELO, Redalyc, DOAJ, Latindex, Dialnet, Google Scholar, LILACS, Imbiomed o JATS genérico) y los **formatos** de salida.
2. Pega o carga el **artículo** (`.txt`, `.md`, `.docx`). Opcional: plantilla HTML de la revista y esquema/notas.
3. Pulsa **Convertir**. Revisa cada pestaña y descarga archivos sueltos o el **ZIP**.

Hace falta conexión la primera vez y siempre que el navegador no tenga en caché las librerías (Mammoth, JSZip, jsPDF desde jsDelivr, con comprobación de integridad SRI).

## Modos de IA
| Modo | Cuándo usarlo |
|---|---|
| **Manual sin API** (por defecto) | Sin saldo ni clave: el programa te da el prompt, lo pegas en DeepSeek web u otra IA, y pegas la respuesta. Admite “continuar” si la IA corta la salida. |
| Anthropic, OpenAI, Gemini, DeepSeek, Groq, OpenRouter | Con API key. Se guarda **una clave por proveedor** en el navegador (localStorage). |

- **Modelo personalizado**: si el proveedor publica un modelo nuevo, escribe su ID exacto en Configuración; tiene prioridad sobre la lista.
- **Continuación automática**: si la IA se queda sin tokens, el programa pide que continúe (hasta 12 veces) y une las partes.
- Cambiar de proveedor en Configuración **no tiene efecto hasta pulsar Guardar**; Cancelar no modifica nada.
- Groq/OpenRouter gratuitos tienen límites de tokens por minuto: artículos largos pueden requerir el modo manual o otro proveedor.

## Entrada Word (.docx)
Se convierte a HTML simplificado conservando **negritas, cursivas, superíndices, subíndices, listas, tablas (con colspan/rowspan) e imágenes**. Las imágenes viajan al HTML, al PDF, al EPUB y al ZIP (`images/`), y también como figuras del XML JATS.

## Qué genera cada formato
- **XML**: según el destino. SciELO/Redalyc/JATS genérico → JATS (en SciELO se usa `sps-1.9` salvo que indiques otra versión en las notas). DOAJ → XML de carga de artículos (`doajArticles.xsd`). Latindex/Dialnet → Dublin Core. Scholar/LILACS/Imbiomed → metadatos específicos.
  - En **JATS**, las tablas se convierten en imágenes PNG (`…-gtN.png`) y las figuras en `…-gfN.png`, referenciadas con `<graphic>`. Opción en Configuración: conservar además la tabla estructurada con `<alternatives>`.
  - Solo los destinos JATS reciben tablas/figuras; los Dublin Core no se tocan.
- **HTML5**: semántico y accesible, con el CSS de la plantilla si la proporcionas.
- **PDF**: A4 de texto seleccionable, con **fuente Unicode incrustada** (DejaVu Serif; símbolos como ≥ ≤ α β μ χ² Δ − se conservan), enlaces, tablas e imágenes. Usa su propio estilo editorial; **no reproduce el CSS** de la plantilla.
- **EPUB 3**: XHTML bien formado, imágenes empaquetadas, índice de contenidos, metadatos y accesibilidad. Validado con epubcheck 5.2.1 sin errores ni avisos en las pruebas.
- **ZIP**: todos los archivos + `README.txt` con avisos de la generación.

## Validación y límites (importante)
- El programa comprueba que el XML esté **bien formado** y revisa su estructura básica (elementos clave, `id` duplicados, `xref` huérfanos) y avisa de discrepancias. **No valida contra la DTD/esquema oficial**: hazlo con `packtools`/`xmllint` (SciELO) o el validador de cada base de datos antes de enviar.
- Las tablas/figuras del XML se emparejan **por orden** con las del HTML; si los recuentos no coinciden verás un aviso en la pestaña *Paquete*.
- Todo lo generado por IA debe ser **revisado por una persona** antes de publicarse.
- Confirma en cada base de datos la versión de esquema vigente (SPS, DOAJ).
- **Privacidad**: en modo manual el texto va a servicios web de terceros. No pegues datos identificables de pacientes ni manuscritos confidenciales sin autorización.
- Las claves API quedan en el navegador del dispositivo; en equipos compartidos, bórralas al terminar.

## Seguridad
Incluye Content-Security-Policy (solo se permiten conexiones a los proveedores de IA), integridad SRI en las librerías, vista previa HTML en iframe sin scripts y no se hacen peticiones de red para imágenes del documento.

## Publicar / APK
- Sube `index.html` a un repositorio y activa GitHub Pages; usa la URL con WebToApp u otro empaquetador.
- Para uso sin conexión estable, lo ideal es descargar Mammoth, JSZip y jsPDF y servirlos junto al `index.html` (ajustando las etiquetas `<script>`; si cambias de versión, recalcula los hashes SRI).

## Registro de cambios (v1.1 → v1.2)
**Corregido**
- PDF: texto científico corrompido (≥, ≤, α, μ…) por fuentes sin Unicode.
- EPUB: no era XHTML válido; ahora pasa epubcheck. Se empaquetan imágenes; `dc:date` usa la fecha del artículo.
- XML: se inyectaban elementos JATS y se perdía `<?xml?>` en destinos Dublin Core.
- `sanitizeGeneratedXML`: regex mal escapada que comía la “s” final y no quitaba etiquetas vacías con atributos; ya no inventa URLs de licencia.
- Configuración: Cancelar modificaba el estado y una sola clave se compartía entre proveedores.
- Sin continuación al cortarse la salida de la IA; un fallo de XML ya no impide generar HTML/PDF/EPUB.
- Prompt de Imbiomed con barras invertidas; resaltado de atributos XML; `escapeHTML` no escapaba comillas.
- Entrada Word perdía formato, tablas e imágenes; figuras del XML quedaban sin archivo.
- Tablas PNG ignoraban colspan/rowspan.
- Prompts DC contradictorios (“todos presentes” vs “omite si falta”); DOAJ ahora usa su esquema de carga.
- Eliminado `html2pdf.js` (no se usaba); modelos actualizados + campo de modelo personalizado; tokens/temperatura validados; paneles de salida se reinician en cada ejecución.

**Añadido**: avisos de estructura XML, opción `<alternatives>`, CSP, SRI, aviso de privacidad, comprobación de librerías al arrancar.

## Licencias
Fuente incrustada en el PDF: DejaVu Serif (Bitstream Vera License, libre para redistribuir). Librerías: Mammoth (BSD-2), JSZip (MIT/GPLv3), jsPDF (MIT).
