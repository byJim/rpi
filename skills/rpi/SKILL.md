---
name: rpi
description: Flujo Spec-Driven Research → Plan → Implement (RPI) para tareas no triviales en cualquier repo. Deja spec.md, research.md y plan.md en specs/<fecha>-<slug>/, pausa para revisión humana entre fases y luego implementa fase por fase contra el plan aprobado. Usar siempre que el usuario pida implementar una feature, endpoint, módulo, pantalla, comando, integración, migración de datos o cambio que cruce varios módulos, o diga "RPI", "research plan implement", "spec driven", "primero investiga", "haz un plan antes de tocar código", o quiera retomar una spec ("sigue con la spec X", "implementa el plan"). No usar para fixes de una línea ni preguntas sueltas.
argument-hint: '<tarea nueva> | <slug existente> [spec|research|plan|implement]'
---

# RPI — Spec → Research → Plan → Implement

El error caro no es una línea mal escrita: es construir lo que no se pidió, cambiar la forma de un dato
y olvidar a quien lo consume, o descubrir a mitad del diff que el código no funcionaba como se creía.
RPI separa **entender** (Research) de **decidir** (Plan) de **ejecutar** (Implement), y deja cada paso
en un archivo que el usuario revisa. Revisar 60 líneas de plan es más barato que revisar 600 de diff.

Los archivos son la memoria. Entre fases conviene `/clear` y retomar con `/rpi <slug>`: el contexto
chico es donde el modelo trabaja mejor, y nada se pierde porque todo lo decidido está escrito.

## Dónde vive

`specs/<AAAA-MM-DD>-<slug>/` en la raíz del repo:

```
spec.md      ← qué y por qué                    (fase 0)
research.md  ← cómo es el código hoy            (fase 1)
plan.md      ← qué cambia, orden, verificación  (fase 2; checklist vivo en fase 3)
```

`slug` = `<modulo-o-dominio>-<descripcion>` en kebab-case (p. ej. `pedidos-cupones`,
`cli-exportar-markdown`). Es también la rama: `feature/<slug>`.

## El proyecto manda, no esta skill

Esta skill no fija stack ni convenciones. Antes de asumir algo, leerlo del repo:

- **Perfil RPI**: si existe `.claude/rpi.md` en la raíz del repo, leerlo al arrancar cualquier fase.
  Trae las reglas propias del proyecto para cada fase (checklist de research, orden de capas, comandos
  de verificación, límites). Se suman a las de esta skill y, donde chocan, manda el perfil.
- **Convenciones y trampas**: `CLAUDE.md` / `AGENTS.md` / `README.md`, el de la raíz y el de cada
  módulo involucrado.
- **Comandos**: los que el proyecto ya define (scripts de `package.json`, `Makefile`, `justfile`,
  tareas de Gradle o Maven, `pyproject.toml`…). No inventar uno que no está.
- **Herramientas**: el gestor de paquetes del lockfile y la versión de runtime que el repo fija. No
  mezclar gestores ni cambiar versiones de pasada.

Si algo de esto todavía no existe (proyecto recién creado), decidirlo es parte del plan de la primera
tarea, con el OK del usuario; no se decide de pasada mientras se implementa.

## Arranque: detectar la fase

Entrada: $ARGUMENTS

- Nombra una fase → esa manda.
- Nombra un slug o carpeta de `specs/` → leer lo que haya y seguir donde quedó:
  sin `research.md` → Fase 1 · sin `plan.md` → Fase 2 · `plan.md` con `- [ ]` pendientes → Fase 3 ·
  todo marcado → está terminada; ofrecer `/code-review`.
- Tarea nueva → Fase 0.

## Cada fase tiene su archivo

Leer **solo** el archivo de la fase actual (en `${CLAUDE_SKILL_DIR}/`) y seguirlo:

| Fase          | Archivo               |
| ------------- | --------------------- |
| 0 — Spec      | `fase-0-spec.md`      |
| 1 — Research  | `fase-1-research.md`  |
| 2 — Plan      | `fase-2-plan.md`      |
| 3 — Implement | `fase-3-implement.md` |

Si en la misma sesión se pasa a la fase siguiente (p. ej. Spec → Research sin pausa), leer su archivo
antes de seguir. No cargar las otras fases "por si acaso": cada regla de más compite por atención con
las de la fase que importa.
