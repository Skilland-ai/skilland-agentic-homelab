# Run 01: Hermes deep research

Fecha: 2026-06-21

## Objetivo

Comprender Hermes con profundidad antes de instalar, configurar o construir sobre él. Entregar mapa de fuentes, notas de aprendizaje, rol en HomeLab, relación Codex/Hermes, glosario, preguntas abiertas, síntesis para Raúl y QA final.

## Archivos leídos

- `AGENTS.md`
- `01_harness/RULES.md`
- `01_harness/STACK.md`
- `01_harness/TASKFLOW.md`
- `02_context/BRIEF.md`
- `02_context/FACTS.md`
- `02_context/CONSTRAINTS.md`
- `02_context/GLOSSARY.md`
- `02_context/LINKS.md`
- `03_specs/now/001_hermes_deep_research.md`
- `00_inbox/hermes_sources.md`
- `shared/skills/ship-output/SKILL.md`
- `shared/skills/qa-review/SKILL.md`

## Fuentes oficiales revisadas

- https://hermes-agent.nousresearch.com/docs
- https://hermes-agent.nousresearch.com/docs/llms.txt
- https://github.com/NousResearch/hermes-agent
- README oficial del repo.
- Instalador oficial `scripts/install.sh`.
- Árbol raíz del repo oficial.
- Docs oficiales de instalación, quickstart, learning path, CLI, configuración, perfiles, seguridad, tools/toolsets, skills, curador, memoria, memory providers, context files, `SOUL.md`, plugins, cron, delegación, kanban, goals, hooks, messaging, Telegram, webhooks, MCP, ACP, API server, dashboard, profile commands y profile distributions.

## Fuentes comunitarias revisadas

Revisadas vía dump local `00_inbox/hermes_sources.md`:

- Hilo X "How to Become a Hermes Agent Operator".
- Hilo X "after 100 days with Hermes".
- Transcripción video "current Hermes setup / 10 hacks".
- Transcripción video Hermes Desktop.
- Hilo X sobre pipelines baratos con `no_agent`, `wakeAgent`, `context_from`.
- Hilo X "15 levels of Hermes Agent".
- Hilo X guía `SOUL.md`.
- Hilo X "8 loops inside Hermes Agent".
- Hilo X "10 Hermes Agent hacks".

## Pendientes

- Abrir X/videos externos solo si hace falta metadata o contenido no incluido en el dump.
- Revisar contenido del repo tercero `ClaudioDrews/memory-os`.
- Verificar instalación, versión y comportamiento real de Hermes en este VPS en una spec posterior.
- Probar cualquier integración Codex-Hermes solo en entorno dummy y con aprobación.

## Aprendizajes clave

Estado: oficial/verificado.

- Hermes es runtime operativo, no solo chat.
- Perfiles separan identidad, memoria, config, skills, cron y sesiones.
- `SOUL.md` es identidad; `AGENTS.md` es contexto de proyecto.
- Memoria built-in vive en `MEMORY.md` y `USER.md` y se inyecta como snapshot por sesión.
- Skills son SOPs bajo demanda y pueden tener aprobación de escritura.
- Cron, `no_agent`, `wakeAgent` y `context_from` son la vía de loops baratos.
- Kanban da cola durable; subagentes son síncronos y no durables.
- Gateway, Telegram y webhooks existen, pero son superficie de riesgo.
- Dashboard oficial ya cubre gran parte del "mission control".

Estado: comunitario/no verificado.

- La comunidad recomienda progresar de prompt a loop a perfil a trigger a mission control.
- Telegram topics como workspaces y perfiles como departamentos son patrones útiles, no decisiones tomadas.
- Claims de precios, versiones, benchmarks y agentes de terceros no son base técnica.

## Riesgos

- Activar canales externos antes de entender seguridad y allowlists.
- Crear arquitectura de perfiles/mission control antes de tener una rutina real.
- Copiar contenido comunitario sin contraste oficial.
- Meter conocimiento estratégico solo en memoria de Hermes y perder trazabilidad git.
- Permitir a Hermes operar fuera del repo sin límites claros.

## Decisiones propuestas

- Siguiente spec: instalación/smoke test local de Hermes sin gateway externo.
- Empezar con setup mínimo tipo Blank Slate.
- Mantener Codex como operador técnico del repo.
- Usar Hermes primero como residente local del HomeLab, con memoria/skills bajo aprobación.
- Posponer Telegram, webhooks, MCPs externos y mission control custom.

## Preguntas abiertas

Ver `02_context/OPEN_QUESTIONS.md`.

## Próxima acción

Crear `03_specs/now/002_hermes_intimacy_install_smoke_test.md` cuando Raúl apruebe pasar de investigación a instalación controlada.

## Checksum inbox

- Antes: `96e85ca66044eafe5606d2cb9eebc29ada5568c0b4da88d34cfd7c951f2f8503`
- Después: `96e85ca66044eafe5606d2cb9eebc29ada5568c0b4da88d34cfd7c951f2f8503`

## QA contra criterios de aceptación

| Criterio | Estado | Evidencia |
|---|---|---|
| Existe `02_context/HERMES_SOURCE_MAP.md` | pass | Archivo creado |
| Existe `02_context/HERMES_LEARNING_NOTES.md` | pass | Archivo creado |
| Existe `02_context/HERMES_ROLE_IN_HOMELAB.md` | pass | Archivo creado |
| Existe `02_context/CODEX_AND_HERMES.md` | pass | Archivo creado |
| Existe `02_context/HERMES_CONCEPTS_GLOSSARY.md` | pass | Archivo creado |
| Existe `02_context/OPEN_QUESTIONS.md` | pass | Archivo creado |
| Existe `04_outputs/2026-06-21_hermes_metagame_initial_synthesis.md` | pass | Archivo creado |
| Existe `03_runs/2026-06-21_hermes_deep_research_run_01.md` | pass | Este archivo |
| `00_inbox/hermes_sources.md` intacto | pass | Checksum antes/después idéntico |
| No se conectaron sistemas externos/productivos | pass | Solo lectura de docs públicas y dump local; no gateway, webhooks, Telegram, Gmail, Drive, CRM ni servicios productivos |
| Todo output está en español salvo nombres técnicos/URLs | pass | Archivos escritos en español |
| Claims técnicos etiquetados | pass | Se usa `oficial/verificado`, `comunitario/no verificado` y `pendiente de verificar` |
| Siguiente acción clara | pass | Spec propuesta de instalación/smoke test local controlado |
