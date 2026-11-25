# Fase 2 — Plan

Un plan que otra sesión, sin memoria de esta, pueda ejecutar sin tomar decisiones.

Leer spec y research completos y releer los archivos que se van a tocar. Si el commit actual difiere
del anotado en research, revisar qué cambió antes de confiar en él. Si el perfil del proyecto
(`.claude/rpi.md`) fija orden de capas, reglas o comandos de verificación, usar esos.

- La solución más chica que cumpla la spec. Reusar lo que research encontró antes de crear algo nuevo.
- Fases de lo que otros consumen hacia quien lo consume, cada una dejando el proyecto verde: contratos y
  formas de datos → persistencia (esquema, migración, datos de prueba) → lógica → puntos de entrada
  (API, comando, UI) → documentación. Saltar las capas que la tarea no toca.
- Un cambio en un contrato o en la forma de un dato nombra a todos los que lo consumen y qué cambia en
  cada uno; si hay datos ya guardados con la forma vieja, el plan dice qué pasa con ellos.
- Migraciones de esquema: con la herramienta del proyecto, nombradas, aplicadas solo en entornos locales
  o de prueba. Nunca contra bases compartidas o remotas.
- Dependencias: primero lo que el lenguaje, el runtime o el repo ya traen. Una dependencia nueva lleva
  nombre, versión y el porqué en el plan; se instala con el gestor del proyecto.
- Seguir lo que el repo ya usa (lenguaje, linter, estructura de carpetas, estilo de nombres).
- Config nueva: variable documentada en el archivo de ejemplo del proyecto (p. ej. `.env.example`) y
  validada al arrancar; el plan nunca copia secretos ni valores reales.
- Proyecto o módulo recién nacido: las decisiones de base (gestor de paquetes, lenguaje, test runner,
  estructura) son la Fase 1 del plan y van en "Enfoque" con su porqué.
- Cero preguntas abiertas: si queda una, preguntarla ahora y no escribir el plan con dudas.

```markdown
# Plan: <título>

Spec: ./spec.md · Research: ./research.md · Rama: feature/<slug>

## Enfoque (≤5 líneas, con el porqué)

## Lo que NO vamos a hacer

## Fase 1 — <módulo>: <qué>

### Cambios

- [ ] `ruta/archivo` — qué cambia (firma, campo, regla)

### Verificación automática

- [ ] comando

### Verificación manual

- [ ] qué probar → resultado esperado

## Fase 2 — …

## Riesgos y rollback
```

## Verificación

Los comandos salen del perfil del proyecto o de lo que el repo ya define (scripts, tareas, `Makefile`),
escritos tal cual se van a ejecutar. Solo los que existan: un comando inventado en el plan es una casilla
que nadie puede marcar.

- Si falta un comando que la tarea necesita (p. ej. no hay cómo correr tests), agregarlo es un cambio del
  plan, no un supuesto.
- Cada fase con lógica nueva lleva al menos un test que falla sin el cambio.
- La verificación manual es concreta: el comando o la URL exacta y lo que debe verse.
- Cierre: todos los comandos de verificación del proyecto, en orden lint → tipos → tests → build.

Pausa: enfoque + lista de fases; pedir aprobación. Sugerir `/clear` y `/rpi <slug>` para implementar.
