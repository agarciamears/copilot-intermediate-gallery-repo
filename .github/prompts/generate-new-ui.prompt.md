# Crear Nuevo Componente UI

Genera un nuevo componente UI para la aplicación de Galería de Fotos & Portafolio siguiendo los patrones establecidos.

## Patrones del Proyecto
- TypeScript con interfaces estrictas
- Patrón de layout: SectionContainer + SectionTitle
- Diseño responsivo con Tailwind CSS
- Soporte para dark mode (clases `dark:`)
- Animaciones con Framer Motion donde sea apropiado
- Iconos de Lucide React
- Accesibilidad (ARIA labels, semántica)

## Requisitos
1. Crear interface TypeScript para props
2. Usar Tailwind classes con variantes dark mode
3. Exportar componente y tipos
4. Convención: PascalCase para componentes
5. Responsive design (mobile-first)

## Ubicación de Archivos
- Componentes de layout: `src/components/ui/layout/`
- Componentes de galería: `src/components/gallery/`
- Componentes de upload: `src/components/upload/`
- Componentes genéricos: `src/components/ui/`

## Patrón de Uso
```tsx
<SectionContainer>
  <SectionTitle title="Nombre del Componente" />
  {/* Contenido */}
</SectionContainer>
```

Sigue estos patrones e incluye ejemplos de uso.