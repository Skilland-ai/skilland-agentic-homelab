# Run 01: Hermes self-guided operator onboarding

Fecha: 2026-06-21

## Objetivo

Que Raúl aprenda a operar Hermes directamente en CLI con el perfil `homelab`, guiado paso a paso en español, priorizando inspección, lectura local read-only, cierre/continuidad de sesión y criterio operativo básico antes de automatismos.

## Archivos leídos

- `AGENTS.md`
- `README.md`
- `03_specs/now/003_hermes_self_guided_operator_onboarding.md`

Como contexto de referencia durante la conversación también se usaron fragmentos de:

- `03_runs/2026-06-21_hermes_intimacy_install_smoke_test_run_01.md`
- `05_scratch/hermes_official/docs/user-guide__configuration.md`
- `05_scratch/hermes_official/docs/user-guide__security.md`
- `05_scratch/hermes_official/docs/user-guide__features__memory.md`
- `05_scratch/hermes_official/docs/user-guide__features__skills.md`

## Comando usado para abrir Hermes

Comando principal usado por Raúl:

```bash
homelab
```

También se practicó continuidad con:

```bash
homelab --continue
```

## Prompt pegado en Hermes

```text
Actua como instructor de Hermes para Skilland Agentic HomeLab. Guiame paso a paso, en espanol, para aprender a operar esta sesion. No ejecutes trabajo autonomo pesado. Antes de cada accion explicame que vamos a comprobar y por que. No conectes sistemas externos, no arranques gateway, no uses cron, webhooks, MCPs externos ni --yolo. No escribas memoria, skills ni archivos salvo que yo lo apruebe explicitamente. Primero lee AGENTS.md, README.md y la spec activa, y luego guiame por los comandos basicos de inspeccion.
```

## Git status inicial

```text
## main...origin/main
 M 03_specs/decisions.md
 D 03_specs/now/001_hermes_deep_research.md
?? 02_context/HERMES_RUNTIME_NOTES.md
?? 03_runs/2026-06-21_hermes_intimacy_install_smoke_test_run_01.md
?? 03_specs/done/
?? 03_specs/now/003_hermes_self_guided_operator_onboarding.md
?? 04_outputs/2026-06-21_hermes_intimacy_install_smoke_test_v1.md
?? 05_scratch/hermes_install/
```

## Preflight fuera de Hermes

Comandos ejecutados por Raúl:

```bash
pwd
git status --short --branch
command -v hermes
command -v homelab || true
hermes --profile homelab profile show homelab
hermes --profile homelab config check
pgrep -af "hermes.*gateway" || true
```

Salidas relevantes sanitizadas:

```text
pwd: /home/skilland/workspaces/skilland-agentic-homelab
hermes: /home/skilland/.local/bin/hermes
homelab: /home/skilland/.local/bin/homelab

Profile: homelab
Path:    /home/skilland/.hermes/profiles/homelab
Model:   gpt-5.4 (openai-codex)
Gateway: stopped
Skills:  0
.env:    exists
SOUL.md: exists
Alias:   homelab → hermes -p homelab  (/home/skilland/.local/bin/homelab)

Config version: 0 → 30 (update available)
Required: none missing
Optional: many external integrations unset (esperado para este microhito)

pgrep mostró procesos `tui_gateway.entry` y `tui_gateway.slash_worker` a pesar de que `profile show` reportó `Gateway: stopped`.
```

## Slash commands practicados

Raúl indicó que los comandos básicos funcionaron correctamente y se dieron por válidos sin pegar todas las salidas por ser muy básicas:

- `/profile`
- `/status`
- `/model`
- `/tools list`
- `/toolsets`
- `/memory pending`
- `/skills pending`
- `/save`
- `/title`
- `/quit`
- `/resume`

Adicionalmente se usó continuidad fuera de Hermes con `homelab --continue`.

## Lectura local read-only practicada

Prompt usado dentro de Hermes:

```text
Lee 02_context/HERMES_RUNTIME_NOTES.md sin modificar archivos. Resume en espanol: estado actual de Hermes, riesgos principales, y que no deberiamos activar todavia.
```

Resumen de la salida observada:

- Hermes está instalado y operativo en el VPS como usuario `skilland`.
- Perfil activo de trabajo: `homelab`.
- Provider/modelo: OpenAI Codex / `gpt-5.4`.
- Gateway parado según perfil; sin canales externos, sin cron y sin browser tooling activado para esta práctica.
- Riesgos principales: terminal local sin sandbox fuerte, auth persistente por perfil, migración de config pendiente v0 → v30, posibilidad de confundir capacidades visibles con aprobaciones reales.
- Recomendación explícita de no activar todavía gateway, canales externos, webhooks, MCPs externos, Playwright/Chromium, Gmail/Drive/CRM/Kapso ni `--yolo`.

## Resumen de lo que Hermes explicó

Durante la práctica guiada, Hermes explicó y reforzó estos puntos:

- Antes de cada bloque conviene verificar contexto real del repo y del perfil, no asumirlo.
- `git status`, `profile show` y `config check` sirven para saber dónde estás parado antes de pedir trabajo.
- Los slash commands básicos permiten inspeccionar perfil, estado, modelo, herramientas, pendientes y continuidad sin tocar sistemas externos.
- Que una capacidad aparezca en `/tools list` o `/toolsets` no implica que deba usarse en esta spec.
- Existe diferencia entre estado declarado por la app y estado observable del sistema; el ejemplo concreto fue `Gateway: stopped` frente a procesos TUI visibles con `pgrep`.
- La lectura local read-only es una capacidad útil y segura para HomeLab.

## Aprobaciones aparecidas, rechazos o pendientes

Durante la práctica guiada no se documentaron aprobaciones manuales de memoria, skills ni edición de archivos dentro de Hermes. Tampoco se aprobaron a ciegas pendientes de memoria o skills.

Más tarde, ya fuera del bloque estricto de onboarding, Raúl decidió reconfigurar el perfil para quitar fricción de aprobaciones.

## Cambio posterior de política de aprobaciones

Después de dar la práctica por buena, Raúl pidió explícitamente quitar prompts de aprobación y ejecutó:

```bash
hermes --profile homelab config set approvals.mode off
hermes --profile homelab config set memory.write_approval false
hermes --profile homelab config set skills.write_approval false
```

Verificación posterior del archivo real:

```yaml
approvals:
  mode: false
memory:
  write_approval: false
skills:
  write_approval: false
```

Observación:

- `approvals.mode` quedó serializado como `false` en `config.yaml`, no como la cadena `off`.
- `memory.write_approval` y `skills.write_approval` quedaron explícitamente en `false`.
- El cambio se considera una decisión posterior del operador, no parte obligatoria del bloque guiado de la spec.

## Fricciones

- Salida muy larga de `hermes --profile homelab config check`, con muchas variables opcionales no relevantes para este microhito.
- La discrepancia entre `Gateway: stopped` y procesos `tui_gateway.*` puede confundir a un operador nuevo.
- `/resume` y `--continue` funcionan, pero pueden reabrir contexto anterior y meter ruido si no se documenta.
- El operador consideró molesto el patrón de aprobación manual por defecto.
- Al cambiar `approvals.mode off`, el CLI mostró `False`, lo que obliga a verificar el archivo real o el comportamiento efectivo.

## Aprendizajes de Raúl

- Ya sabe abrir Hermes con `homelab` y retomar sesión con `homelab --continue`.
- Ya sabe hacer un preflight mínimo del repo y del perfil antes de empezar.
- Entiende para qué sirven los slash commands básicos de inspección y continuidad.
- Entiende que ver una herramienta disponible no equivale a tener permiso o necesidad de usarla.
- Detectó una preferencia operativa clara: menos fricción en aprobaciones, incluso a costa de más riesgo.

## QA contra criterios de aceptación

- [x] Existe `03_runs/2026-06-21_hermes_self_guided_operator_onboarding_run_01.md`.
- [x] Existe `04_outputs/2026-06-21_hermes_self_guided_operator_onboarding_v1.md`.
- [x] Raúl operó Hermes directamente en CLI.
- [x] Hermes actuó como guía paso a paso, no como ejecutor autónomo pesado.
- [x] Todo el output escrito queda en español.
- [x] Se practicaron al menos 6 slash commands.
- [x] Hermes leyó contexto del repo y explicó límites correctamente.
- [x] Se hizo una tarea read-only sobre `02_context/HERMES_RUNTIME_NOTES.md`.
- [x] No se usó `--yolo`.
- [x] No se arrancó Gateway.
- [x] No se conectaron canales externos.
- [x] No se configuraron webhooks.
- [x] No se configuraron cron jobs.
- [x] No se configuraron MCPs externos.
- [x] No se tocaron sistemas productivos.
- [x] No se aprobaron memorias, skills ni escrituras de archivos a ciegas durante la práctica guiada.
- [x] Si hubo revisión de pendientes, no se aprobó nada a ciegas.
- [x] `00_inbox/hermes_sources.md` queda intacto.
- [x] La recomendación del siguiente microhito queda clara.

## Riesgos

- Hermes corre con permisos reales del usuario `skilland`; el CLI no es un sandbox fuerte.
- El perfil `homelab` quedó después en un modo mucho más permisivo para aprobaciones y escrituras.
- La continuidad de sesión puede arrastrar contexto anterior si no se usa con cuidado.
- La migración de config v0 → v30 sigue pendiente.
- La presencia de toolsets externos visibles puede tentar a usarlos antes de tiempo.

## Preguntas abiertas

- ¿Conviene mantener `homelab` en modo sin fricción total o reservar ese ajuste para perfiles más desechables?
- ¿Hace falta una chuleta corta permanente de slash commands y preflight para HomeLab?
- ¿La próxima práctica debe entrar ya en memoria/skills o primero conviene consolidar una segunda sesión de operación básica?

## Siguiente acción recomendada

Planificar `004_hermes_profile_memory_skill_lab`, pero redefiniendo antes el criterio operativo de aprobaciones: decidir si `homelab` se queda como perfil rápido sin fricción o si se reserva un perfil separado para pruebas más peligrosas.
