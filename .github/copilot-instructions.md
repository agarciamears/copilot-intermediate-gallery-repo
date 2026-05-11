# Instrucciones para Copilot - Galería de Fotos y Portafolio

## 📋 ¿Qué son estas instrucciones?
Las instrucciones de Copilot son directivas que definen el contexto, patrones y mejores prácticas para un proyecto específico. Copilot las usa para:

- Generar código coherente con la arquitectura existente
- Mantener convenciones consistentes
- Evitar anti-patterns en el proyecto
- Acelerar desarrollo al "recordar" decisiones de diseño

## 🎯 Descripción del Proyecto
Este es un proyecto real: una Galería de Fotos y Portafolio profesional.

Propósito: demostrar características de GitHub Copilot en una aplicación Next.js moderna.

Esta es una aplicación de Galería de Fotos y Portafolio profesional construida con Next.js 15, TypeScript y Tailwind CSS. La aplicación sigue una arquitectura orientada a componentes con:

- **Interacciones en Cliente** usando React hooks y animaciones Framer Motion
- **Componentes Inteligentes** para layout y estilos consistentes
- **Patrón Mock Data** para desarrollo y pruebas sin API real
- **Sistema de Diseño Responsivo** usando Tailwind CSS

## 🏗️ Arquitectura del Proyecto

### Componentes Principales
¿Por qué esta estructura? Para reutilización y claridad.

1. **Componentes de Layout** (`src/components/ui/layout/`)
   - `Hero.tsx` - Encabezados de página (título + descripción grande)
   - `SectionContainer.tsx` - Envoltorio consistente para secciones
   - `SectionTitle.tsx` - Títulos de sección con opción de "Ver Todo"

2. **Componentes de Características**
   - `UploadZone.tsx` - Zona drag & drop con preview en tiempo real
   - `GalleryGrid.tsx` - Grid responsivo de fotos con filtrado y paginación
   - `StatsGrid.tsx` - Panel de estadísticas
   - `FeatureCard.tsx` - Tarjetas reutilizables para destacar características

### 🔄 Flujo de Datos
Importante: ¿cómo viaja la información en esta app?

- **Mock data** vive en `src/lib/` = datos ficticios (no de API real)
- **State management** = React hooks (useState, useEffect)
- **Props de componentes** = parámetros tipados con TypeScript
- **Transformaciones** ocurren EN el componente

### 📂 Estructura de Proyecto
```
src/
├── app/                # Next.js 15 App Router - DEFINICIÓN DE RUTAS
│   ├── page.tsx        # / (página inicio)
│   ├── gallery/page.tsx    # /gallery (galería)
│   ├── upload/page.tsx     # /upload (subir fotos)
│   ├── admin/page.tsx      # /admin (panel de control)
│   └── layout.tsx      # Layout global (header, footer)
│
├── components/         # Código React reutilizable
│   ├── ui/             # Componentes genéricos (layout, tarjetas, stats)
│   ├── gallery/        # Componentes específicos para galería
│   └── upload/         # Componentes específicos para upload
│
└── lib/                # Lógica y datos
    ├── mock-photo-data.ts
    ├── mock-admin-data.ts
    ├── mock-feature-card-data.ts
    └── mock-tag-data.ts
```

## 🎨 Patrones de Componentes

### 1️⃣ Componentes de Layout
Regla: siempre estructura las secciones así para mantener consistencia.

```tsx
<SectionContainer>
  <SectionTitle title="Nombre de la Sección" viewAllLink="/optional-link" />
  {/* Contenido aquí */}
</SectionContainer>
```

### 2️⃣ Tarjetas de Características
Regla: para destacar features o acciones, usa siempre este componente.

```tsx
<FeatureCard
  icon={IconComponent}
  title="Título de Feature"
  description="Descripción"
  iconColor="text-blue-600"
/>
```

### 3️⃣ Mostrar Estadísticas
Regla: para números o KPIs, usa siempre `StatsGrid`.

```tsx
<StatsGrid stats={[
  {
    label: "Fotos Totales",
    value: "1,234",
    icon: FolderOpen,
    color: 'blue'
  }
]} />
```

## 🎯 Convenciones de Estilos

### ✅ REGLA 1: Colores con Dark Mode
Tailwind + Dark Mode = escribir dos clases.

```tsx
{/* ✅ BIEN */}
<div className="text-slate-900 dark:text-white">
  Funciona en light mode y dark mode
</div>

{/* ❌ MAL: solo light mode */}
<div className="text-slate-900">
  De noche es invisible
</div>
```

### ✅ REGLA 2: Patrón de Fondo Gradiente
Este proyecto usa un gradiente estándar en todas las páginas.

```tsx
{/* ✅ BIEN */}
<div className="page-gradient">
  <Hero ... />
</div>
```

### ✅ REGLA 3: Espaciado Consistente
Usa siempre estas clases.

```tsx
<div className="container mx-auto px-4">
<div className="grid md:grid-cols-3 gap-6">
```

## 🚀 Flujo de Desarrollo

### Cómo correr el proyecto
```bash
npm run dev  # Inicia servidor con Turbopack
```

### Archivos clave para APRENDER el proyecto
- `COMPONENT_USAGE_GUIDE.md` - Ejemplos reales de cada componente
- `mock-*-data.ts` - Estructuras de datos
- `page.tsx` en cada ruta - Cómo se ARMAN las páginas

## ✨ Mejores Prácticas

### 1️⃣ TypeScript (Tipado Fuerte)
Regla: cada componente debe tener una interfaz clara.

```tsx
{/* ✅ BIEN: interface explícita */}
interface FeatureCardProps {
  icon: LucideIcon;
  title: string;
  description: string;
  iconColor: string;
}

export function FeatureCard({ icon: Icon, title, description, iconColor }: FeatureCardProps) {
  // TypeScript SABE qué tipos son
}
```

### 2️⃣ Diseño de Componentes
Regla: un componente = una responsabilidad (SRP).

```tsx
{/* ✅ BIEN: componente solo MUESTRA */}
export function FeatureCard({ icon, title, description, iconColor }: FeatureCardProps) {
  return <div className="card-feature">{/* ... */}</div>;
}
```

### 3️⃣ State Management
Regla: mantén el state cerca de donde se usa.

```tsx
{/* ✅ BIEN */}
export default function GalleryPage() {
  const [selectedTags, setSelectedTags] = useState<string[]>([]);
  
  return (
    <>
      <FilterPanel onChange={setSelectedTags} />
      <GalleryGrid selectedTags={selectedTags} />
    </>
  );
}
```

### 4️⃣ Estilos (CSS/Tailwind)
Regla: usa clases de Tailwind, no CSS custom innecesario.

```tsx
{/* ✅ BIEN: Tailwind puro */}
<button className="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg">
  Click
</button>

{/* ✅ MEJOR: Clase reutilizable en globals.css */}
<button className="btn-primary">Click</button>
```

## ⚠️ Antipatrones (Lo que NUNCA hacer)

### ❌ Componentes que Hacen Demasiado
Lógica de fetch, estado, filtrado y presentación todo en un mismo componente = pesadilla.

```tsx
{/* ❌ MAL */}
export function GalleryGrid() {
  const [photos, setPhotos] = useState([]);
  const [filtered, setFiltered] = useState([]);
  useEffect(() => { fetch('/api/photos')... }); // Fetch aquí
  // Filtrado aquí, animaciones aquí, 200 líneas de HTML... TODO EN UNO
}

{/* ✅ BIEN */}
export default function GalleryPage() {
  const photos = usePhotos(); // Fetch en custom hook
  return <GalleryGrid photos={photos} />; // Solo muestra
}
```

### ❌ Props Drilling
Pasar props a través de 5 niveles de componentes que no los usan.

```tsx
{/* ❌ MAL: Page → Section → Container → FilterPanel */}
<Page tags={tags}><Section tags={tags}><FilterPanel tags={tags} /></Section></Page>

{/* ✅ BIEN */}
<FilterPanel tags={tags} /> {/* Donde se necesita, punto */}
```


Siempre respóndeme como experto en esta tecnología y no asumas nada. Si tienes dudas, haz preguntas para aclarar el contexto antes de responder. Siempre responde en español.

La generación de commits debe ser siempre en español y descriptiva.
