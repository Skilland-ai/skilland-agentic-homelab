# Hermes: síntesis inicial del metagame para Raúl

Fecha: 2026-06-21

## Lectura corta

Estado: oficial/verificado.

Hermes no es "otro chat". Es un runtime de agente: CLI/TUI, memoria, skills, perfiles, cron, gateway, kanban, dashboard, MCP, API y ACP. La oportunidad para Skilland no es conversar con Hermes; es convertirlo en una capa operativa interna que recuerde, ejecute rutinas, coordine perfiles y deje trazabilidad.

Estado: comunitario/no verificado.

El metagame de la comunidad va en una dirección consistente: pasar de prompts sueltos a loops. Primero una rutina aburrida, luego perfil especialista, luego cron, luego trigger, luego visibilidad tipo mission control. Esa secuencia es útil, pero no hay que copiar claims de precios, dashboards custom o flotas de agentes sin prueba local.

## Qué es verdad oficial vs comunidad

Estado: oficial/verificado.

Oficialmente existen los ladrillos importantes: perfiles separados, `SOUL.md`, `MEMORY.md`, `USER.md`, context files, skills, curador, cron, `no_agent`, `wakeAgent`, `context_from`, `/goal`, subagentes, kanban, gateway, Telegram, webhooks, dashboard, MCP, API server, ACP y distribuciones de perfiles.

Estado: comunitario/no verificado.

Comunidad aporta playbooks: Telegram topics como workspace, mission control, perfiles como departamentos, skills como SOPs, loops de bajo costo y agentes especialistas. Eso es estrategia, no prueba. Skilland debe copiar el orden mental, no las implementaciones completas.

## Patrones de más leverage

Estado: oficial/verificado.

1. Skills como SOPs: cada rutina repetida puede volverse procedimiento versionable.
2. Cron barato: `no_agent`, `wakeAgent` y `context_from` permiten automatizar sin gastar tokens en cada tick.
3. Perfiles: separan memoria, identidad, config, cron y skills por función.
4. Kanban: da cola durable y handoffs cuando subagentes síncronos no bastan.
5. Dashboard: ya existe una sala de máquinas oficial; no hace falta inventarla primero.

## Qué debería copiar Skilland

Estado: pendiente de verificar.

- Empezar con un perfil HomeLab local, no con Telegram.
- Mantener Codex como operador técnico y usar Hermes como runtime/memoria/coordinación cuando esté probado.
- Convertir aprendizajes en archivos de repo antes de meterlos en memoria de agente.
- Crear skills solo después de ejecutar una rutina real.
- Diseñar loops pequeños que escriban outputs revisables.

## Qué debería evitar

Estado: pendiente de verificar.

- No construir mission control custom todavía.
- No conectar Gmail, Drive, CRM, WhatsApp, Telegram, Slack, Discord ni webhooks productivos.
- No crear diez perfiles antes de tener una operación.
- No mover memoria estratégica solo a `MEMORY.md`; lo importante debe quedar versionado.
- No aceptar claims comunitarios de costo/modelo/versión sin benchmark.

## Ruta de aprendizaje recomendada

Estado: pendiente de verificar.

1. Instalar Hermes de forma controlada y verificar CLI/doctor/modelo.
2. Crear perfil HomeLab mínimo con `SOUL.md`, cwd limitado al repo y aprobaciones para memoria/skills.
3. Probar contexto: que lea `AGENTS.md` y una spec pequeña sin tocar sistemas externos.
4. Probar una skill simple derivada de un procedimiento real.
5. Probar un cron local sin agente o con `wakeAgent`, que escriba a archivo.
6. Observar dashboard/kanban antes de diseñar UI propia.

## Próximos 3 microhitos

Estado: pendiente de verificar.

1. `002_hermes_intimacy_install_smoke_test`: instalación local controlada, Blank Slate, `hermes doctor`, primer chat CLI, contexto del repo y cero canales externos.
2. `003_hermes_profile_memory_skill_lab`: perfil HomeLab, `SOUL.md` mínimo, memoria/skills con aprobación, una skill real y QA de aislamiento.
3. `004_hermes_local_loop_lab`: cron local con `no_agent` o `wakeAgent`, output en repo/scratch, sin Telegram/webhooks/MCP externos.

## Ideas HomeLab más fuertes

Estado: comunitario/no verificado con mecanismos oficiales/verificados.

- "Residente de laboratorio": Hermes vive como agente interno del HomeLab, no como producto externo.
- "Departamentos después de rutina": perfiles solo cuando una función ya existe.
- "SOP vivo": skills nacen de tareas repetidas y verificadas.
- "Loops antes que dashboards": primero rutina, luego visibilidad.
- "Codex mano técnica, Hermes memoria/control": Codex ejecuta en repo; Hermes coordina cuando haya runtime validado.

## Conclusión

Estado: pendiente de verificar.

La jugada correcta no es instalar todo Hermes ni construir un cockpit. Es ganarse intimidad con el runtime: una instalación limpia, una conversación controlada, una memoria aprobada, una skill útil y un cron local barato. Si eso funciona, Hermes puede convertirse en el núcleo operativo del HomeLab.
