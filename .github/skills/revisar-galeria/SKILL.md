---
name: revisar-galeria
description: Revisa cambios de la galería de este workshop para detectar regresiones en filtros, búsqueda, likes y Load More. Úsala al revisar GalleryGrid o GalleryPage y sus componentes extraídos.
disable-model-invocation: true
---
# Revisar el contrato de la galería

Produce una revisión basada en el código disponible. No edites la aplicación ni instales dependencias durante esta revisión.

1. Lee `src/components/gallery/GalleryGrid.tsx`, `src/app/gallery/page.tsx` y `src/lib/mock-photo-data.ts`. Si se extrajo PhotoCard, inspecciona su implementación y punto de uso.
2. Determina qué revisar: el diff indicado por el usuario o, si no existe diff, el estado actual. No inventes una rama base ni afirmes comparar cambios en una carpeta sin historial Git.
3. Lee [el contrato y los casos](references/contrato-galeria.md). Contrasta cada comportamiento con la implementación; señala los cambios deliberados de contrato como decisiones que requieren confirmación del instructor.
4. Sigue el flujo padre → props → cálculo → render → interacción. Verifica dónde viven los likes, dónde se reinicia currentPage y qué parte es solo simulada.
5. Separa defectos sustentados, riesgos que necesitan ejecución y preferencias. Para cada hallazgo aporta archivo, fragmento o línea real, consecuencia y corrección mínima propuesta.
6. Describe las comprobaciones manuales pendientes. Solo ejecuta comandos o pruebas si el usuario lo solicita y existe la configuración necesaria. Nunca declares un resultado exitoso que no observaste.

## Formato de salida

- Alcance: archivos leídos y base de comparación, o «revisión del estado actual».
- Tabla: criterio | evidencia en código | resultado (conservado, cambiado, no comprobado).
- Hallazgos priorizados con evidencia y propuesta mínima.
- Comprobaciones ejecutadas y resultados; después, comprobaciones pendientes.
- Conclusión acotada: qué se puede sostener con la evidencia disponible.

Si faltan archivos, identifica cuáles y limita la conclusión. Usa español. Una ausencia de hallazgos no demuestra ausencia de errores.
