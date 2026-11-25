# rpi

Spec-Driven Development con Research, Plan, Implement (RPI): **Spec → Research → Plan → Implement**.

Cada fase deja un archivo en `specs/<AAAA-MM-DD>-<slug>/` de tu repo:

| Fase          | Archivo       | Qué contiene                                              |
| ------------- | ------------- | --------------------------------------------------------- |
| 0 — Spec      | `spec.md`     | Qué se quiere y por qué, criterios de aceptación, alcance |
| 1 — Research  | `research.md` | Cómo funciona hoy el código que la tarea toca             |
| 2 — Plan      | `plan.md`     | Qué cambia, en qué orden y cómo se verifica               |
| 3 — Implement | `plan.md`     | El mismo plan, usado como checklist vivo                  |

Las ideas:

- Proporcionar un flujo de trabajo para programación agéntica.
- Los archivos buscan ser la memoria y la fuente de verdad, así que entre fases puedes hacer `/clear` y retomar con `/rpi <slug>` sin perder nada.
- Funciona muy bien con un agente `coordinador` y en otra sesión se arranca con `/rpi` (próximamente skill `coordinar`).

## Instalación

Como plugin en Claude Code:

```
/plugin marketplace add byJim/rpi
/plugin install rpi@byjim
```

O desde la terminal:

```bash
claude plugin marketplace add byJim/rpi
claude plugin install rpi@byjim
```

Sin plugin: copia la carpeta `skills/rpi/` a `~/.claude/skills/rpi/` (para todos tus proyectos) o a
`.claude/skills/rpi/` dentro de un repo.

## Uso

```
/rpi agregar cupones de descuento al checkout     ← tarea nueva: empieza en Spec
/rpi pedidos-cupones                              ← retoma la spec donde quedó
/rpi pedidos-cupones plan                         ← fuerza una fase
```

Instalada como plugin también responde a `/rpi:rpi`.

La skill detecta la fase por lo que ya existe en la carpeta de la spec: sin `research.md` investiga, sin
`plan.md` planea, con casillas `- [ ]` pendientes implementa.

## Perfil del proyecto (opcional)

La skill no fija stack. Lee las convenciones de tu repo (`CLAUDE.md`, `AGENTS.md`, `README.md`) y usa los
comandos que el proyecto ya define. Si quieres reglas propias para RPI, créalas en `.claude/rpi.md` en la
raíz del repo: la skill lo lee al arrancar cada fase y, donde choca con sus valores por defecto, manda el
perfil.

Sirve para fijar, por ejemplo, la checklist de research de tu arquitectura, el orden de capas del plan,
los comandos exactos de verificación por paquete y los límites de la fase de implementación. Hay una
plantilla en [`examples/rpi.md`](examples/rpi.md).

## Actualizar

```bash
claude plugin marketplace update byjim
claude plugin update rpi@byjim
```

Los cambios de cada versión están en [`CHANGELOG.md`](CHANGELOG.md).

## Inspiración

La idea de trabajar en fases Research → Plan → Implement la tomé del curso
[rpi-course](https://github.com/CodelyTV/rpi-course) de CodelyTV (tienen excelente contenido).

## Licencia

MIT. Ver [`LICENSE`](LICENSE).
