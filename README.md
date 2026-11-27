# Editorial Suite — corrección XML por revista

Reemplaza el `index.html` de tu repositorio por el de este ZIP.

## Qué se corrigió

- **SciELO/SPS:** el XML final queda con `specific-use="sps-1.9"`, `dtd-version="1.1"` y namespace `xlink`.
- **MEDISAN:** si el título de la revista es MEDISAN, el programa completa el perfil verificado de la revista: `journal-id` `san`, ISSN epub `1029-3019`, publisher `Centro Provincial de Ciencias Médicas` y licencia CC BY 4.0.
- **Tablas SciELO:** la IA debe entregar la tabla completa como `<table>` estructurada; el programa genera la imagen `gtN` y deja el XML final con `<graphic>` dentro del ZIP. Así no quedan referencias a imágenes inexistentes.
- **Redalyc/JATS4R:** ya no recibe las reglas gráficas de SciELO; las tablas quedan como `<table>` estructurada y se retira `specific-use="sps-1.9"` si aparece.
- **Validación:** además de XML bien formado, el programa avisa si faltan elementos clave de SciELO/SPS o si una tabla Redalyc quedó sin tabla estructurada.
- **ORCID:** se normaliza a iD desnudo, como en el paquete MEDISAN publicado de referencia.
- **Elementos vacíos:** se retiran elementos vacíos sin atributos que no deben viajar en el XML.

## Uso

1. Descomprime el ZIP.
2. Reemplaza el `index.html` de tu repositorio por el nuevo.
3. Para MEDISAN/SciELO, genera también el HTML o deja que el programa genere los gráficos desde el XML con tablas estructuradas.
4. Sube a la revista el ZIP completo generado por Editorial Suite, no el XML suelto si el XML referencia imágenes `gt`.
