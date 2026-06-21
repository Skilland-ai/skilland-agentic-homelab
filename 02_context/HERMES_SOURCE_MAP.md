# Mapa de fuentes Hermes

Fecha: 2026-06-21

## Criterio de confianza

- `oficial/verificado`: documentación, `llms.txt`, README, instalador o estructura del repositorio oficial de Nous Research.
- `comunitario/no verificado`: hilos, videos, playbooks o repos de terceros. Sirven para estrategia y patrones, no para afirmar funcionamiento sin contraste oficial.
- `pendiente de verificar`: fuente identificada pero no leída completa, o afirmación que requiere revisar código/docs oficiales antes de usarse.

## Fuentes oficiales primarias

| Fuente | URL | Tipo | Prioridad | Estado de revisión | Utilidad | Verificación pendiente |
|---|---|---:|---:|---|---|---|
| Docs oficiales Hermes Agent | https://hermes-agent.nousresearch.com/docs | Documentación oficial | P0 | revisada vía `llms.txt` y markdowns oficiales | Base técnica para instalación, CLI, perfiles, seguridad, memoria, skills, cron, delegación, kanban, gateway, MCP, API, ACP y dashboard | No para conceptos cubiertos; sí para cambios futuros de versión |
| `llms.txt` oficial | https://hermes-agent.nousresearch.com/docs/llms.txt | Índice oficial para agentes | P0 | revisada | Mapa rápido de la superficie completa de Hermes | No |
| Repositorio oficial | https://github.com/NousResearch/hermes-agent | Código y docs fuente | P0 | revisado vía README, instalador, árbol raíz y docs markdown | Verifica estructura real del proyecto y módulos existentes | Revisar código específico antes de tocar implementación |

## Referencias oficiales revisadas

| Referencia | Tipo | Estado | Uso principal |
|---|---|---|---|
| `README.md` del repo oficial | oficial/verificado | revisada | Identidad de Hermes, capacidades principales, comandos iniciales, gateway y modelo operativo |
| `scripts/install.sh` del repo oficial | oficial/verificado | revisada | Confirmar que el instalador instala dependencias, repo, entorno y comando global |
| Árbol raíz del repo oficial | oficial/verificado | revisada | Confirmar existencia de `agent/`, `gateway/`, `cron/`, `skills/`, `plugins/`, `tools/`, `web/`, `acp_adapter/`, `tests/` |
| Docs `installation`, `quickstart`, `learning-path` | oficial/verificado | revisada | Camino recomendado: CLI estable primero, luego capas |
| Docs `cli`, `slash-commands`, `cli-commands` | oficial/verificado | revisada | TUI, flags, comandos, `/goal`, `/compress`, `/usage`, `/background` |
| Docs `profiles`, `profile-commands`, `profile-distributions` | oficial/verificado | revisada | Perfiles aislados por home, aliases, distribución por git, exclusión de secretos/memorias |
| Docs `security` | oficial/verificado | revisada | Allowlists, aprobaciones, bloqueo de comandos peligrosos, no usar canales abiertos con terminal |
| Docs `personality`, `context-files` | oficial/verificado | revisada | `SOUL.md`, `AGENTS.md`, orden de carga y separación identidad/proyecto |
| Docs `memory`, `memory-providers` | oficial/verificado | revisada | `MEMORY.md`, `USER.md`, memoria congelada por sesión, proveedores externos |
| Docs `skills`, `curator` | oficial/verificado | revisada | Skills como procedimientos, staging/aprobación, curador recuperable |
| Docs `cron`, `automate-with-cron` | oficial/verificado | revisada | Scheduler, `no_agent`, `wakeAgent`, `context_from`, toolsets por job |
| Docs `delegation` | oficial/verificado | revisada | Subagentes síncronos con contexto aislado y toolsets restringidos |
| Docs `kanban` | oficial/verificado | revisada | Board SQLite durable, dispatcher, perfiles trabajadores, dashboard/plugin |
| Docs `messaging`, `telegram`, `webhooks` | oficial/verificado | revisada | Gateway, Telegram, webhooks, allowlists, entrega y riesgos |
| Docs `mcp`, `toolsets-reference`, `tool-search` | oficial/verificado | revisada | MCPs, exposición de herramientas, toolsets ligeros y búsqueda diferida |
| Docs `api-server`, `acp`, `web-dashboard` | oficial/verificado | revisada | API OpenAI-compatible, integración IDE/ACP y dashboard web local/remoto |

## Fuentes comunitarias del dump local

Fuente local preservada: `00_inbox/hermes_sources.md`.

| Fuente | URL | Tipo | Prioridad | Estado de revisión | Utilidad | Necesita verificación oficial |
|---|---|---:|---:|---|---|---|
| Fuente 1: "How to Become a Hermes Agent Operator" | https://x.com/mikenevermiss/status/2063489268169728513 | Hilo X / playbook | P1 | revisada vía dump local | Mentalidad de operador, perfiles, skills, SOUL, cron, Telegram, delegación, revisión de habilidades | Sí; varios conceptos ya confirmados, detalles operativos/precios/modelos no |
| Fuente 2: "after 100 days with Hermes" | https://x.com/sharbel/status/2067257256215789785 | Hilo X / metagame | P1 | revisada vía dump local | Orden de adopción: loops aburridos, workspace Telegram, especialista, cron, trigger, mission control | Sí; usar como inspiración, no como arquitectura final |
| Fuente 3: video "current Hermes setup / 10 hacks" | https://www.youtube.com/watch?v=FpIvl6b4tRo | Video / tutorial | P2 | revisada vía transcripción local | Mission control, Notion triggers, cron, `/goal`, subagentes, kanban, webhooks, perfiles | Sí; video externo no abierto completo |
| Fuente 4: video Hermes Desktop | https://www.youtube.com/watch?v=2pIihd3dpoA | Video / tutorial | P2 | revisada vía transcripción local | Desktop como superficie operativa, gateway, skills, toolsets, perfiles | Sí; Desktop y dashboard tienen base oficial, detalles del video no |
| Fuente 4 duplicada: MemoryOS | https://github.com/ClaudioDrews/memory-os | Repo tercero | P3 | pendiente de verificar | Posible inspiración para memoria/wiki | Sí; no usar como verdad Hermes |
| Fuente 5: pipelines baratos | https://x.com/tonbistudio/status/2068559870589079552 | Hilo X / patrón técnico | P1 | revisada vía dump local | `no_agent`, `wakeAgent`, `context_from` para reducir tokens | Parcial: esos tres mecanismos están confirmados oficialmente; ejemplos concretos no |
| Fuente 6: "15 levels of Hermes Agent" | https://x.com/IBuzovskyi/status/2068629714776756339 | Hilo X / mapa de madurez | P1 | revisada vía dump local | Gradiente de madurez: chatbot, memoria, skills, MCP, subagentes, perfiles, kanban, API, ACP, distribuciones | Sí; categorías confirmadas, claims de versión, precios y benchmarks no |
| Fuente 7: guía `SOUL.md` | https://x.com/IBuzovskyi/status/2065125711401062758?s=20 | Hilo X / guía | P1 | revisada vía dump local | Cómo pensar identidad del agente y separar `SOUL.md` de instrucciones de proyecto | Parcial: la arquitectura de `SOUL.md` está confirmada; plantillas/opiniones no |
| Fuente 8: "8 loops inside Hermes Agent" | https://x.com/IBuzovskyi/status/2064377155476193362?s=20 | Hilo X / metagame | P1 | revisada vía dump local | Loops: objetivo, skills, curador, memoria, kanban, compresión, subagentes | Sí; loops existen en docs, narrativas comparativas no |
| Fuente 9: "10 Hermes Agent hacks" | https://x.com/IBuzovskyi/status/2062101068842975409?s=20 | Hilo X / recetas | P1 | revisada vía dump local | Ideas fuertes para HomeLab: control room, cron, goal, subagentes, Telegram topics, kanban, SOPs, webhooks | Sí; usar solo después de validar cada mecanismo |

## Pendientes

- Abrir los X/videos externos solo si se necesita metadata exacta o contenido no incluido en el dump local. Estado: pendiente de verificar.
- Revisar el repo `ClaudioDrews/memory-os` antes de copiar cualquier patrón. Estado: pendiente de verificar.
- Verificar contra código oficial antes de afirmar detalles internos no cubiertos por docs. Estado: pendiente de verificar.
- Confirmar versión instalada de Hermes en el VPS solo en una spec de instalación. Estado: pendiente de verificar.
