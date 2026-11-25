# Fase 0 — Spec

Acordar el problema antes de mirar código. Escribir `spec.md` con lo que dijo el usuario; lo que falte
y cambie el resultado, preguntarlo (AskUserQuestion, máx. 4 preguntas). Lo demás, asumirlo y anotarlo
como supuesto.

Si ya hay una spec relacionada en `specs/` (misma zona, tarea previa de la que esta depende), enlazarla:
sus decisiones siguen valiendo salvo que esta spec diga lo contrario. Si el perfil del proyecto
(`.claude/rpi.md`) nombra otras fuentes para la spec (un documento de diseño, un ticket, un handoff),
buscarlas y enlazarlas también.

```markdown
# <Título>

## Problema / por qué

## Comportamiento esperado

(desde quien lo usa: persona en la interfaz o en la terminal, otro servicio, tarea programada)

## Criterios de aceptación

- [ ] observable y verificable

## Alcance

Módulos / carpetas: … · Datos que se leen o escriben: … · Servicios externos / APIs: sí/no (cuáles) ·
Dependencias nuevas: sí/no · Config o secretos nuevos: sí/no

## Supuestos

## Fuera de alcance
```

Si hubo preguntas o supuestos fuertes, pausar y pedir OK. Si la tarea venía clara, seguir directo a
Research (leer `fase-1-research.md`): el usuario revisa spec y research juntos.
