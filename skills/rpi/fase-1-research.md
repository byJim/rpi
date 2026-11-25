# Fase 1 — Research

Documentar cómo funciona **hoy** lo que la tarea toca. Research describe; no propone soluciones ni
critica el código. Las opiniones metidas aquí se cuelan al plan como decisiones que nadie revisó.

## Preguntas primero, código después

Quien investiga sabiendo qué se quiere construir encuentra lo que espera encontrar. Por eso la spec se
traduce a **preguntas sobre el código actual** y los subagentes reciben solo esas preguntas: nunca
`spec.md`, el título de la tarea ni lo que se quiere lograr.

Una buena pregunta pide hechos (dónde, cómo, qué existe) y no lleva la solución dentro:

- Mal: "¿Cómo agrego el endpoint de cupones?" · Bien: "¿Qué rutas, esquemas y tablas existen hoy para
  cupones, con `archivo:línea`?"
- Mal: "¿Dónde conecto la API nueva?" · Bien: "¿Qué servicios externos se llaman hoy, desde qué módulo,
  con qué manejo de errores y reintentos, y qué tests lo cubren?"

## Pasos

1. Leer `spec.md`, el perfil del proyecto (`.claude/rpi.md`) si existe, y `CLAUDE.md` / `AGENTS.md` /
   `README.md` de la raíz y de cada módulo involucrado: ahí están las convenciones y las trampas conocidas.
2. Escribir las preguntas en `research.md`, sección "Preguntas", antes de lanzar nada.
3. Investigar. Si la zona es chica (un puñado de archivos), leerla directamente. Si cruza varios módulos,
   lanzar subagentes `Explore` en paralelo, uno por módulo, cada uno con sus preguntas y nada más. Pedirles
   flujo y rutas `archivo:línea`, no volcados de archivos ni recomendaciones.
4. Verificar en persona los 2–3 hallazgos críticos; no firmar el resumen de un subagente a ciegas.
5. ¿Hace falta ver datos o respuestas reales de un servicio? Solo lectura (en bases de datos, solo
   `SELECT`), con las herramientas que el perfil o el repo indiquen, y nunca copiar secretos ni datos
   personales a `research.md`.
6. Si la tarea depende de una librería o API externa, anotar la versión instalada (manifiesto + lockfile)
   y comprobar su comportamiento en la documentación de **esa** versión, no de memoria.

Si lo que la tarea toca todavía no existe (proyecto o módulo nuevo), eso es un hallazgo, no un permiso
para saltarse la fase: research documenta entonces qué hay alrededor (estructura, convenciones,
dependencias, comandos) y qué falta por decidir, que pasa a "Preguntas abiertas".

## Checklist fija

`research.md` responde cada punto (con "no aplica" o "no existe aún" si corresponde; omitirlo esconde el
hueco). Si el perfil del proyecto trae su propia checklist, sus puntos se agregan a estos:

- **Flujo actual** punta a punta con `archivo:línea`: punto de entrada (pantalla, ruta HTTP, comando,
  tarea programada, import público) → lógica → datos / servicios externos → salida.
- **Contratos y formas de datos**: tipos, esquemas de validación y formatos que se tocan o faltan, y
  quién los consume.
- **Persistencia**: dónde viven los datos (base de datos, archivos, almacenamiento externo), cómo se
  migra su esquema y qué pasa con los datos existentes si cambia su forma.
- **Auth y permisos**: quién puede llegar a esta zona hoy y qué lo comprueba.
- **Servicios externos y eventos**: qué APIs se llaman, con qué cliente, límites, errores y reintentos;
  qué eventos, colas o notificaciones se emiten y dónde.
- **Config y secretos**: qué variables de entorno se leen y dónde se validan (nombres, nunca valores).
- **Piezas reutilizables**: helpers, utilidades, componentes, clientes ya escritos.
- **Tests** que ya cubren la zona y con qué comando se corren.
- **Preguntas abiertas**.

```markdown
# Research: <título>

Fecha · commit (`git rev-parse --short HEAD`, o "sin git")

## Resumen (≤5 líneas)

## Preguntas

## Flujo actual

## Hallazgos (checklist)

## Preguntas abiertas
```

Pausa: resumen + preguntas abiertas. Sugerir `/clear` y `/rpi <slug>` para planear con contexto limpio.
