# Fase 3 — Implement

Ejecutar el plan aprobado, no rediseñarlo.

1. Leer `plan.md` y `spec.md`. Las casillas marcadas valen: seguir desde la primera pendiente.
2. Estado del repo: `git status -sb`. En la rama principal → crear `feature/<slug>`. Si hay cambios
   ajenos sin commitear, avisar antes de tocar nada. Si el proyecto no es un repo git, decirlo y
   preguntar si se inicializa (`git init`); no hacerlo por cuenta propia.
3. Entorno: dependencias instaladas con el gestor del proyecto y, si el plan depende de un servicio
   local (base de datos, contenedor, emulador), confirmar que está arriba antes de empezar.
4. Por fase: cambio → marcar `- [x]` en `plan.md` apenas se termina (es lo que permite retomar tras un
   `/clear`) → verificación automática → arreglar hasta verde.
5. Fin de fase: reportar la verificación automática y la lista manual, y esperar OK antes de la siguiente,
   salvo que el usuario haya pedido ir de corrido.
6. Si el código no coincide con el plan o aparece algo no previsto: parar, explicar esperado vs encontrado,
   proponer el ajuste y actualizar `plan.md` con el OK del usuario. El plan es el registro de lo decidido;
   improvisar en silencio lo vuelve mentira.

Límites que en esta fase es fácil pisar (el perfil del proyecto, `.claude/rpi.md`, puede agregar los suyos):

- Commit/push/PR solo si el usuario lo pide, con la convención de mensajes del repo. Nunca
  `git push --force`.
- Dependencias: solo las que nombra el plan, con el gestor del proyecto. Una que no estaba prevista es
  un desvío del plan (punto 6), no un `install` de pasada.
- Secretos: nunca leer `.env` ni copiar valores a archivos, specs o memoria. Los nombres de variables
  van en el archivo de ejemplo.
- Nada destructivo sin OK explícito: reiniciar o borrar bases de datos, migraciones contra entornos
  remotos, borrar datos o contenido generado, sobrescribir archivos del usuario, llamadas a servicios
  externos que publican, envían o cobran. Para probarlas, usar el modo de prueba que el plan haya definido.
- No "arreglar" de paso código fuera del plan: se anota como pendiente en el resumen final.

Cierre: todo marcado + resumen por módulo de qué cambió y qué quedó pendiente de verificación manual.
Ofrecer `/code-review`.
