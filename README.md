# Editorial Suite — XML ajustado por base de datos

Versión ajustada según la investigación de formatos de intercambio:

- **SciELO:** XML de texto completo **SPS sobre JATS**. Para MEDISAN se mantiene `specific-use="sps-1.9"` del paquete publicado de referencia; otra versión SPS solo si la colección la confirma. Las tablas se convierten a gráficos `gtN` solo en SciELO y el paquete ZIP debe subirse completo.
- **DOAJ:** **DOAJ Native XML** de metadatos (`records/record`). No es XML de texto completo. El programa advierte si faltan `journalTitle`, `publicationDate`, `title`, `fullTextUrl` o ISSN/EISSN.
- **Redalyc/AmeliCA:** XML de texto completo **JATS/JATS4R**, con tablas estructuradas `<table>` y sin `specific-use` de SciELO.
- **Latindex:** metadatos **OAI-PMH + Dublin Core** (`oai_dc`) para interoperabilidad; no es carga JATS.
- **Dialnet:** metadatos **OAI-PMH Dublin Core** (`oai_dc`) normalizados para cosecha.
- **LILACS:** registro bibliográfico **LILACS/FI-Admin** con descriptores DeCS/MeSH; no es JATS de texto completo.
- **Imbiomed:** ficha de metadatos. No se afirma un XML oficial porque no hay esquema público verificable.
- **Google Scholar:** no acepta carga XML. El resultado operativo son las etiquetas HTML `citation_*`; el archivo XML generado es solo referencia.
- **Genérico JATS:** **JATS 1.4** de texto completo, con `dtd-version="1.4"`.

Uso: reemplaza el `index.html` del repositorio por el de este ZIP. Genera el paquete completo y sube el ZIP cuando el destino incluya gráficos referenciados, especialmente en SciELO.
