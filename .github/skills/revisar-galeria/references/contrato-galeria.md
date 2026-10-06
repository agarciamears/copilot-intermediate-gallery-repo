# Contrato didáctico de la galería

Punto de partida: copia local proporcionada para el workshop, revisada el 6 de octubre de 2026. Este contrato describe esa implementación, no una especificación oficial de GitHub ni el resultado de pruebas ejecutadas.

| Criterio | Comportamiento de partida | Caso para comprobar |
|---|---|---|
| Tags | OR entre tags seleccionados mediante `some`; sin tags no se restringe por tag | Seleccionar dos tags; una foto que coincide con cualquiera puede permanecer |
| Búsqueda | Coincidencia parcial sin distinguir mayúsculas en título, tags o fotógrafo | Buscar un texto existente con mayúsculas y minúsculas |
| Combinación | Resultado de tags AND resultado de búsqueda | Un texto coincidente no debe anular el filtro de tags |
| Load More | Acumula desde índice 0 hasta `currentPage * limit` | Caso hipotético: 14 coincidencias, limit=6, páginas 1/2/3 muestran 6/12/14 |
| Cambio de filtro | GalleryPage reinicia currentPage a 1 | Cargar más y luego cambiar búsqueda o tag |
| Likes | Set local por ID; segundo clic deshace; mockPhotos no se muta | Marcar, desmarcar, filtrar y volver mientras el padre siga montado |
| Datos | Photo y mockPhotos se importan de src/lib/mock-photo-data.ts | No asumir prop photos ni API de fotos que no existen |
| Límites | Detalles y carga son simulados; no hay persistencia de likes | No prometer conservación después de recargar la página |

Para cantidades reales usa el dataset que esté abierto. Las 14 coincidencias del ejemplo son hipotéticas; no las presentes como un conteo medido. Si el instructor agregó mocks, recalcula el total.

Una extracción de PhotoCard debe conservar callbacks, estado en el padre, animación y uso del tipo Photo existente. Las mejoras de accesibilidad son propuestas distintas de una refactorización puramente estructural.
