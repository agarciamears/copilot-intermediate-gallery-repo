# Demo: Crear un Agente Personalizado para Bicep IaC

¡Bienvenido a este demo de creación de agentes personalizados con GitHub Copilot! Aprenderás a crear desde cero un modo de agente especializado en Infrastructure as Code con Azure Bicep, sin escribir una sola línea de código de aplicación.

---

## Lo que Aprenderás
Al finalizar este demo, podrás:
- [ ] Entender la diferencia entre un modo de agente y Copilot por defecto
- [ ] Conocer la estructura de un archivo `.agent.md`
- [ ] Crear un agente especializado en Bicep IaC desde cero en VS Code
- [ ] Activar el agente en Copilot Chat y ver el cambio de comportamiento en tiempo real
- [ ] Evaluar cuándo vale la pena crear un agente para tu equipo

**Tiempo Estimado:** 10-15 minutos

---

## Contexto: ¿Qué es un Modo de Agente Personalizado?

Un modo de agente es un archivo Markdown que vive en `.github/agents/` y redefine cómo se comporta GitHub Copilot cuando ese modo está activo. Puedes pensar en él como una persona especializada dentro de Copilot: mismas capacidades base, comportamiento diferente.

**Archivo de ejemplo ya en este repo:**
```
.github/agents/Plan.agent.md
```
Abre ese archivo ahora y revisa su estructura antes de continuar.

### Anatomía de un archivo `.agent.md`

```markdown
---
name: NombreDelAgente
description: Descripción breve que aparece en el selector de Copilot
tools: ['search/codebase', 'web/fetch']
focusArea: 'Área de especialización'
---

# Nombre del Agente

## Instructions
Aquí van las instrucciones de comportamiento en lenguaje natural.
```

- El bloque `---` (frontmatter) controla metadatos y herramientas disponibles.
- El cuerpo en Markdown define las instrucciones de comportamiento.
- No hay código, no hay compilación, no hay despliegue.

---

## 🎯 Paso 1: Entiende el Problema que Vamos a Resolver

**El problema:** Copilot por defecto genera Bicep funcional, pero sin seguir estándares de equipo. No pregunta el entorno, no aplica defaults de seguridad, no referencia Azure Verified Modules (AVM).

**La solución:** Un agente `BicepArchitect` que actúa como un senior de infraestructura con los estándares de tu organización ya incorporados.

**Resultado esperado:** La audiencia entiende que el valor no es solo automatizar, sino especializar el comportamiento para los estándares reales de un equipo.

---

## ✍️ Paso 2: Crea el Archivo del Agente en VS Code

### Opción A: Copilot lo crea por ti (recomendada para demo en vivo)

1. Abre GitHub Copilot Chat en modo `Agent`
2. Escribe el siguiente prompt:

```markdown
Crea un archivo de agente personalizado en `.github/agents/BicepArchitect.agent.md`.

Quiero un agente experto en Azure Bicep e IaC con estas características:
- Antes de generar código, siempre pregunta: naming convention, entorno y scope de despliegue
- Prefiere Azure Verified Modules (AVM) cuando existan
- Parametriza todo lo que cambia entre entornos
- Añade descripción a cada parámetro con @description()
- Aplica defaults de seguridad: Storage sin acceso público, TLS 1.2, Key Vault con soft delete
- Nunca hardcodea secretos
- Explica cada recurso que genera y avisa si hay implicaciones de coste o seguridad
- Solo genera Bicep, nunca ARM JSON
```

3. Revisa el archivo generado y ajusta si es necesario.

### Opción B: Lo escribes manualmente (para explicar la estructura)

1. Crea el archivo `.github/agents/BicepArchitect.agent.md`
2. Añade el frontmatter con `name`, `description`, `tools` y `focusArea`
3. Escribe las instrucciones en el cuerpo del archivo

**💡 Tip para la demo:** La Opción A es más impactante visualmente, pero la Opción B permite explicar cada campo con detalle.

**Resultado esperado:** El archivo `.github/agents/BicepArchitect.agent.md` existe en el repo.

---

## 🔄 Paso 3: Activa el Agente y Observa el Cambio

1. Abre GitHub Copilot Chat en VS Code
2. Haz click en el selector de modo (donde dice `Ask`, `Edit`, `Agent`, etc.)
3. Selecciona **BicepArchitect** de la lista
4. Escribe el siguiente prompt:

```markdown
Necesito un Storage Account con acceso privado y una lifecycle policy que mueva blobs a cool tier después de 30 días.
```

### Qué observar con la audiencia

- ¿Copilot pregunta el entorno y la naming convention antes de generar?
- ¿Aplica `allowBlobPublicAccess: false` y `minimumTlsVersion: 'TLS1_2'` sin que se lo pidas?
- ¿Incluye el parámetro `tags` con descripción?
- ¿Avisa del coste de la lifecycle policy?
- ¿Incluye el comando de despliegue al final?

**Resultado esperado:** Comportamiento claramente diferente al de Copilot por defecto.

---

## 🆚 Paso 4: Compara con Copilot por Defecto (Opcional)

Para hacer el contraste más evidente:

1. Cambia el modo de vuelta a `Agent` (modo por defecto)
2. Envía exactamente el mismo prompt
3. Compara las respuestas lado a lado

**Puntos de discusión con la audiencia:**

- ¿Qué diferencias notas en el resultado?
- ¿Cuánto tiempo te ahorraría tener un agente así en tu equipo?
- ¿Qué otros agentes crearías para tus flujos de trabajo?

---

## 🧠 Puntos de Mensaje para la Audiencia

- Un agente personalizado no requiere código: solo Markdown con instrucciones en lenguaje natural.
- Los estándares de tu equipo (naming, seguridad, AVM) se pueden codificar una vez y reutilizar siempre.
- Cualquier persona del equipo puede crear o mejorar un agente — no es trabajo exclusivo de ingeniería.
- Un agente vive en el repo junto al código, se versiona con Git y se comparte con todo el equipo automáticamente.

---

## 💡 Ideas de Agentes para tu Equipo

| Nombre | Propósito |
|---|---|
| `BicepArchitect` | IaC con estándares de seguridad y AVM |
| `SecurityReviewer` | Revisión de código enfocada en OWASP Top 10 |
| `APIDesigner` | Diseño de APIs REST con OpenAPI 3.0 |
| `TestWriter` | Generación de tests siguiendo la convención del proyecto |
| `PRReviewer` | Revisión de pull requests con criterios de equipo |

---

## ✅ Lista de Verificación de Completitud

Marca cada ítem al completarlo:

- [ ] Revisé el agente `Plan.agent.md` existente para entender la estructura
- [ ] Creé el archivo `.github/agents/BicepArchitect.agent.md`
- [ ] Activé el agente en Copilot Chat y lo probé con un prompt real
- [ ] Comparé el resultado con Copilot en modo por defecto
- [ ] Identifiqué al menos un agente adicional que sería útil para mi equipo

---

## 🚀 ¿Qué Sigue?

Los agentes personalizados y los servidores MCP se complementan:

- **Agente**: define *cómo piensa* Copilot para una tarea
- **MCP Server**: define *qué puede hacer* Copilot sobre sistemas externos

Prueba combinar los dos: activa `BicepArchitect` y, si tienes conectado el servidor MCP de GitHub, pídele que además cree el issue con el plan de infraestructura.

👉 **[Ver Demo de GitHub MCP: de Issue a Pull Request](./github-mcp-issue-to-pr-demo.md)**
