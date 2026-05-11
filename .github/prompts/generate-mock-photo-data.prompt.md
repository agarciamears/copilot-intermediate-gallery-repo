# Generar Datos Mock de Fotos

Genera entradas adicionales de datos mock de fotos para la aplicación de galería de fotos. Los datos deben seguir la estructura existente en `mock-photo-data.ts`.

## Instrucciones

1. ¿Cuántas entradas nuevas de fotos te gustaría agregar a los datos mock? (Por favor especifica un número)

## Referencia de Estructura de Datos
Cada entrada de foto debe incluir:
```typescript
{
  id: string;          // Identificador único
  url: string;         // Ruta a la foto (formato: '/placeholder-{número}.jpg')
  title: string;       // Título descriptivo
  tags: string[];      // Array de etiquetas relevantes
  likes: number;       // Número de likes (rango: 50-500)
  downloads: number;   // Número de descargas (rango: 20-200)
  views: number;       // Número de vistas (rango: 500-5000)
  photographer: string;// Nombre del fotógrafo
  dateTaken: string;   // Formato de fecha ISO (YYYY-MM-DD)
}
```

## Requisitos
- Cada entrada debe tener IDs únicos continuando desde el último ID en los datos existentes
- Las URLs deben seguir el patrón '/placeholder-{número}.jpg'
- Incluir categorías diversas de fotos (paisaje, retrato, arquitectura, naturaleza, etc.)
- Usar números de engagement realistas (likes, descargas, vistas)
- Incluir fechas dentro de los últimos 6 meses
- Proporcionar nombres de fotógrafos variados pero realistas
- Incluir 3-5 etiquetas relevantes por foto

## Ejemplo de Entrada
```typescript
{
  id: '10',
  url: '/placeholder-10.jpg',
  title: 'Valle de Niebla Matutina',
  tags: ['paisaje', 'mañana', 'niebla', 'naturaleza'],
  likes: 178,
  downloads: 67,
  views: 1843,
  photographer: 'Rachel Green',
  dateTaken: '2024-01-20'
}
```

Por favor proporciona el número de entradas que te gustaría generar, y te ayudaré a crear nuevos datos mock que cumplan con estos requisitos.
