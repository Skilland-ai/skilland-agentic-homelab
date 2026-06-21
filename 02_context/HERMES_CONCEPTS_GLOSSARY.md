# Glosario Hermes

Fecha: 2026-06-21

- Hermes Agent: agente de Nous Research con CLI/TUI, memoria, skills, herramientas, perfiles, cron, gateway, kanban, MCP, API y dashboard. Estado: oficial/verificado.
- CLI/TUI: interfaz terminal interactiva de Hermes para chat, herramientas, slash commands, sesiones, modelos y aprobaciones. Estado: oficial/verificado.
- Desktop: aplicación nativa de Hermes que puede usar backend local o remoto vía dashboard. Estado: oficial/verificado.
- Gateway: proceso de Hermes que conecta plataformas de mensajería, mantiene sesiones por canal y ejecuta scheduler de cron. Estado: oficial/verificado.
- Profile: home separado de Hermes con config, `.env`, `SOUL.md`, memoria, sesiones, skills, cron y gateway state propios. Estado: oficial/verificado.
- Profile distribution: repo git que empaqueta un agente completo para instalarlo/actualizarlo sin incluir secretos, memorias ni sesiones. Estado: oficial/verificado.
- `SOUL.md`: archivo de identidad/persona estable del agente, separado de reglas de proyecto. Estado: oficial/verificado.
- `AGENTS.md`: archivo de instrucciones de proyecto/código que Hermes y Codex pueden usar como contexto operativo. Estado: oficial/verificado.
- `MEMORY.md`: memoria de agente con notas, hechos de entorno y lecciones. Estado: oficial/verificado.
- `USER.md`: memoria de preferencias/perfil del usuario. Estado: oficial/verificado.
- Skill: paquete de procedimiento/conocimiento que Hermes carga bajo demanda y puede exponer como slash command. Estado: oficial/verificado.
- Skill curator: mantenimiento de skills generadas por agente; archiva y consolida sin borrar automáticamente. Estado: oficial/verificado.
- Toolset: grupo de herramientas habilitadas para una sesión, plataforma o job. Estado: oficial/verificado.
- Tool Search: mecanismo para diferir esquemas de herramientas MCP/plugin y reducir carga de contexto cuando hay muchas herramientas. Estado: oficial/verificado.
- Cron job: tarea programada de Hermes, one-shot o recurrente, que corre en sesión aislada bajo scheduler. Estado: oficial/verificado.
- `no_agent`: modo de cron script-only, sin LLM ni tokens. Estado: oficial/verificado.
- `wakeAgent`: salida JSON de script que decide si un cron job despierta al agente. Estado: oficial/verificado.
- `context_from`: conexión entre la salida reciente de un cron job y el contexto de otro. Estado: oficial/verificado.
- `/goal`: objetivo persistente que puede continuar entre turnos con juez auxiliar. Estado: oficial/verificado.
- Slash command: comando conversacional como `/model`, `/tools`, `/skills`, `/compress`, `/usage`, `/goal`. Estado: oficial/verificado.
- Subagent: agente hijo creado por delegación, con contexto aislado y toolsets restringidos. Estado: oficial/verificado.
- Delegation: mecanismo para dividir una tarea y recibir un resumen final de subagentes. Estado: oficial/verificado.
- Kanban: tablero durable SQLite para tareas, perfiles trabajadores, dispatcher, comentarios, dependencias e historial. Estado: oficial/verificado.
- Dispatcher: proceso que reclama y ejecuta tareas kanban para perfiles trabajadores. Estado: oficial/verificado.
- Webhook: endpoint del gateway que recibe eventos externos, valida firma/secreto y los transforma en prompts o entregas. Estado: oficial/verificado.
- Hook: sistema de extensiones para gateway, plugins o shell que reacciona a eventos internos. Estado: oficial/verificado.
- MCP: Model Context Protocol; conexión de Hermes a servidores externos de herramientas por stdio o HTTP. Estado: oficial/verificado.
- API server: servidor HTTP compatible con OpenAI que expone chat, responses, runs, jobs y sesiones de Hermes. Estado: oficial/verificado.
- ACP: Agent Client Protocol para integrar Hermes con editores/IDEs. Estado: oficial/verificado.
- Dashboard: UI web oficial para gestionar configuración, API keys, memoria, sesiones, logs, cron, skills, MCPs, webhooks, perfiles y chat. Estado: oficial/verificado.
- Mission control: patrón comunitario de sala de control que combina dashboard, kanban, cron, perfiles y canales. Estado: comunitario/no verificado.
- Telegram topics/workspaces: patrón de usar threads o grupos como superficies separadas de trabajo. Base Telegram oficial; patrón workspace comunitario. Estado: comunitario/no verificado.
- Obsidian/wiki memory: patrón de base de conocimiento en archivos/notas; Hermes documenta memoria y algunos ejemplos de notas, pero el diseño wiki HomeLab queda por definir. Estado: pendiente de verificar.
- Blank Slate: modo de setup mínimo con pocas herramientas y capas avanzadas desactivadas. Estado: oficial/verificado.
- Prompt cache/memoria congelada: la memoria built-in se inyecta como snapshot al inicio de sesión para preservar contexto estable. Estado: oficial/verificado.
