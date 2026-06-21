# Notas de aprendizaje Hermes

Fecha: 2026-06-21

## Qué es Hermes

Estado: oficial/verificado.

Hermes Agent es un agente de Nous Research orientado a tareas reales, terminal, memoria persistente, skills, herramientas, gateway de mensajería y despliegue en máquina local, VPS o backends aislados. No debe tratarse como un chatbot simple: la documentación oficial lo presenta como un runtime de agente con CLI/TUI, scheduler, memoria, perfiles, tools, MCP, API, ACP y superficies de operación.

## No es solo chatbot

Estado: oficial/verificado.

La CLI permite conversación interactiva, pero Hermes también ejecuta herramientas, conserva memoria, crea o actualiza skills, programa cron jobs, delega a subagentes, opera tableros kanban, expone API y gateway. El aprendizaje correcto para Skilland es empezar por chat CLI controlado, pero entenderlo como capa operativa.

## CLI, Desktop y Gateway

Estado: oficial/verificado.

La CLI/TUI es la superficie base para sesiones, slash commands, selección de modelo, herramientas, skills y trabajo técnico. Desktop existe como interfaz nativa y puede conectarse a backend remoto mediante dashboard. El Gateway es un proceso separado para plataformas de mensajería, cron y sesiones por canal; conecta Telegram, Discord, Slack, WhatsApp, Signal, Email y otros adaptadores cuando se configuran.

Estado: pendiente de verificar.

No se verificó ninguna instalación local ni conexión real de Desktop/Gateway en este VPS. La spec prohíbe activar canales externos.

## Perfiles

Estado: oficial/verificado.

Un perfil es un home separado de Hermes con su propio `config.yaml`, `.env`, `SOUL.md`, memorias, sesiones, skills, cron jobs y estado de gateway. Los perfiles permiten modelar especialistas o departamentos, pero no son sandbox de filesystem por sí mismos; si se necesita limitar el trabajo hay que configurar directorios, toolsets y aprobaciones.

## `SOUL.md`

Estado: oficial/verificado.

`SOUL.md` define identidad, tono y comportamiento estable del agente. Vive en `HERMES_HOME`, se carga como parte primaria del prompt de sistema y no debe usarse para reglas de proyecto. Las reglas de proyecto pertenecen en `AGENTS.md` o `.hermes.md`.

## `MEMORY.md` y `USER.md`

Estado: oficial/verificado.

Hermes usa memoria incorporada en dos archivos: `MEMORY.md` para notas del agente, entorno y lecciones, y `USER.md` para preferencias o perfil del usuario. La memoria se inyecta como snapshot al inicio de la sesión; cambios escritos durante una sesión aparecen en la siguiente. Se puede exigir aprobación para escrituras de memoria.

## `AGENTS.md` y contexto de proyecto

Estado: oficial/verificado.

Hermes reconoce archivos de contexto como `.hermes.md`, `HERMES.md`, `AGENTS.md`, `CLAUDE.md`, `.cursorrules` y reglas de Cursor. En arranque de sesión elige un tipo de contexto de proyecto por prioridad, y `SOUL.md` queda separado como identidad. Subdirectorios con `AGENTS.md` pueden descubrirse de forma perezosa durante llamadas a herramientas.

## Skills

Estado: oficial/verificado.

Las skills son conocimiento operativo bajo demanda, normalmente con `SKILL.md`, procedimiento, errores comunes y verificación. Hermes puede instalarlas, cargarlas como slash commands, agruparlas en bundles y proponer nuevas skills tras resolver tareas complejas. Con `skills.write_approval` las escrituras quedan staged antes de aprobarse.

## Curador de skills

Estado: oficial/verificado.

El curador mantiene skills generadas por el agente, identifica uso activo o stale, archiva de forma recuperable y puede consolidar con LLM si se activa. No elimina automáticamente. Esto importa para HomeLab porque evita que el aprendizaje operativo se convierta en basura permanente.

## Cron

Estado: oficial/verificado.

Hermes puede programar trabajos one-shot o recurrentes. Cada job corre en sesión fresca y aislada bajo el scheduler del gateway. Los prompts deben ser autocontenidos. Los jobs pueden adjuntar skills, workdir, toolsets y destino de entrega.

## Controles de costo en cron

Estado: oficial/verificado.

`no_agent=True` ejecuta solo script y entrega stdout sin LLM. `wakeAgent` permite que un script decida si despierta al agente. `context_from` conecta la salida reciente de un job con el prompt de otro. Estos tres mecanismos son clave para loops baratos y observables.

Estado: comunitario/no verificado.

La fuente comunitaria de pipelines baratos propone patrones de producto alrededor de esos mecanismos. Los mecanismos están confirmados, pero los ejemplos concretos y promesas de costo no se adoptan sin prueba local.

## `/goal`

Estado: oficial/verificado.

`/goal` mantiene un objetivo persistente entre turnos. Un juez auxiliar decide si continuar o cerrar; hay comandos para estado, pausa, resume y clear. Sirve para objetivos largos, pero no reemplaza una spec escrita ni un QA explícito.

## Slash commands

Estado: oficial/verificado.

Hermes incluye slash commands para ayuda, modelos, herramientas, skills, background tasks, voz, razonamiento, estado, sesiones, compresión y más. Los comandos son una interfaz de control, no solo atajos de chat.

## Subagentes y delegación

Estado: oficial/verificado.

`delegate_task` crea agentes hijos con contexto aislado, toolsets restringidos y resumen final devuelto al padre. La delegación es síncrona y no durable; si el padre se interrumpe, los hijos se cancelan. Para trabajos durables conviene cron o kanban.

## Kanban

Estado: oficial/verificado.

Kanban es un tablero SQLite durable compartido entre perfiles. Soporta tareas, estados, comentarios, dependencias, dispatcher y perfiles trabajadores. A diferencia de `delegate_task`, el kanban conserva cola, historial y handoffs, por lo que encaja mejor con operaciones repetibles y humanas en el loop.

## Gateway y mensajería

Estado: oficial/verificado.

El gateway mantiene conexiones a plataformas de mensajería, sesiones por chat, scheduler de cron y entrega de respuestas. Por seguridad, los usuarios no están autorizados por defecto; se usan allowlists, pairing y configuración por plataforma.

Estado: pendiente de verificar.

No se activó gateway ni canal externo. Cualquier conexión a Telegram, Slack, WhatsApp, Email o similar requiere aprobación humana explícita y una spec de seguridad.

## Telegram, workspaces y topics

Estado: oficial/verificado.

La documentación oficial cubre bot de Telegram, tokens de BotFather, allowlists de IDs numéricos, DMs, grupos, privacy mode, home channel y thread ID para cron. Telegram puede ser una superficie de control, pero también amplía el riesgo porque da acceso conversacional a un agente con herramientas.

Estado: comunitario/no verificado.

Las fuentes comunitarias recomiendan usar topics como workspaces y separar flujos por proyecto. Es un patrón útil para pensar, pero todavía no se aplica al HomeLab.

## Webhooks y triggers de eventos

Estado: oficial/verificado.

El adapter de webhooks del gateway recibe POSTs, valida firmas/HMAC cuando corresponde, transforma payloads a prompts y puede entregar resultados. También existe un sistema de hooks para gateway, plugins y shell hooks.

Estado: pendiente de verificar.

No hay webhook conectado. Antes de activar uno hay que definir secreto, allowlist, payload mínimo, destino y modo `deliver_only` si no hace falta LLM.

## Mission control y dashboard

Estado: oficial/verificado.

Hermes trae `hermes dashboard`, una UI web local para configuración, API keys, MCPs, webhooks, gateway, memoria, sesiones, logs, analytics, cron, skills y perfiles. También expone chat TUI embebido. Por defecto corre en `127.0.0.1`; si se expone fuera de loopback entran requisitos de autenticación.

Estado: comunitario/no verificado.

"Mission control" en fuentes comunitarias parece una capa operativa custom sobre dashboard, kanban, cron y perfiles. Para Skilland debe ser inspiración posterior, no primer entregable.

## MCPs

Estado: oficial/verificado.

Hermes puede conectar MCPs por stdio o HTTP, con catálogo opcional y controles de include/exclude. Los MCPs amplían herramientas y también superficie de riesgo. El preset `codex` existe si el CLI de Codex está en PATH, pero no se probó localmente.

## API server

Estado: oficial/verificado.

Hermes puede exponer un endpoint HTTP compatible con OpenAI para chat, responses, models, capabilities, runs, jobs y sesiones. Requiere activar server y clave. Es útil para UIs o control planes, pero no hace falta para alfabetización inicial.

## IDE y ACP

Estado: oficial/verificado.

Hermes puede operar como servidor ACP para editores como VS Code, Zed o JetBrains. Usa la misma config, credenciales, skills y estado que CLI. El toolset `hermes-acp` está orientado a workflows de editor y excluye ciertas capacidades de mensajería/cron.

## Distribuciones de perfiles

Estado: oficial/verificado.

Una distribución empaqueta un agente completo como repo git: `SOUL.md`, config, skills, cron, MCP y manifest `distribution.yaml`. Excluye secretos, memorias, sesiones e historial. Encaja para compartir agentes especializados cuando Skilland ya tenga perfiles estables, no en el primer microhito.

## Memoria, wiki y base de conocimiento tipo Obsidian

Estado: oficial/verificado.

Hermes trae memoria built-in y proveedores externos como Honcho, OpenViking, Mem0, Hindsight, Holographic, RetainDB, ByteRover y Supermemory. Kanban y cron documentan patrones de diario largo y notas tipo Obsidian.

Estado: comunitario/no verificado.

La idea de una wiki/Obsidian como cerebro operativo aparece fuerte en fuentes comunitarias. Puede inspirar el HomeLab, pero debe implementarse primero como archivos locales simples y verificables, no como sistema de memoria complejo.

## Modelos, toolsets y control de tokens

Estado: oficial/verificado.

Hermes permite seleccionar proveedor/modelo, usar toolsets por sesión o job, usar setup Blank Slate, activar Tool Search para reducir carga de esquemas, comprimir sesiones largas con `/compress`, revisar uso con `/usage`, usar modelos auxiliares y asignar modelos más baratos en subagentes o jueces.

Estado: comunitario/no verificado.

Las fuentes comunitarias hacen claims sobre precios, versiones concretas y combinaciones de modelos. Esos claims no se aceptan como verdad para Skilland sin benchmark local.

## Lectura estratégica para Skilland

Estado: comunitario/no verificado.

El metagame comunitario coincide en una secuencia: primero loop pequeño y aburrido, luego perfil especialista, luego schedule, luego trigger, luego visibilidad. Es una buena heurística porque evita construir dashboard antes de saber qué operación debe mostrar.

Estado: oficial/verificado.

La documentación oficial respalda que esos ladrillos existen. La decisión de producto y orden de adopción sigue siendo de Skilland.
