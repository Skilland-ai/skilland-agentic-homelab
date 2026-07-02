# Run 01: cierre formal 004 Hermes identity/memory foundation

Fecha: 2026-07-02

## Objetivo

Cerrar formalmente la spec 004 tras la aplicación y verificación de la v1.1 estratégica de identidad/memoria del perfil Hermes `homelab`.

No se buscó rediseñar identidad ni abrir diagnóstico estratégico nuevo. Esta run fue QA final, limpieza menor, documentación de cierre y archivo de spec.

## Archivos leídos

- `AGENTS.md`
- `01_harness/RULES.md`
- `01_harness/STACK.md`
- `01_harness/TASKFLOW.md`
- `03_specs/now/004_hermes_identity_memory_foundation.md`
- `03_runs/2026-06-21_hermes_identity_memory_foundation_run_01.md`
- `03_runs/2026-07-02_hermes_identity_memory_v1_1_run_01.md`
- `04_outputs/2026-06-21_hermes_identity_memory_foundation_v1.md`
- `02_context/HERMES_PROFILE_FOUNDATION.md`
- `02_context/HERMES_RUNTIME_NOTES.md`
- `03_specs/decisions.md`

## Estado inicial

Comandos:

```bash
git status --short --branch
find 03_specs/now -maxdepth 1 -type f -print | sort
```

Resultado:

```text
## main...origin/main
 M 02_context/HERMES_PROFILE_FOUNDATION.md
?? .hermes/
?? 03_runs/2026-07-02_hermes_identity_memory_v1_1_run_01.md
?? 04_outputs/2026-07-02_hermes_identity_memory_v1_1_audit.md
?? 04_outputs/2026-07-02_punto_situacion_homelab_v1.md
?? 05_scratch/2026-07-02_004_hermes_identity_memory_v1_1_implementation_spec.md
?? 05_scratch/hermes_identity_memory_v1_1_before/

03_specs/now/.keep
03_specs/now/004_hermes_identity_memory_foundation.md
```

Observación: 004 era la única spec activa además de `.keep`.

## Verificación final del perfil Hermes `homelab`

Comando:

```bash
wc -c /home/skilland/.hermes/profiles/homelab/SOUL.md \
  /home/skilland/.hermes/profiles/homelab/memories/MEMORY.md \
  /home/skilland/.hermes/profiles/homelab/memories/USER.md
```

Resultado:

```text
3091 /home/skilland/.hermes/profiles/homelab/SOUL.md
1814 /home/skilland/.hermes/profiles/homelab/memories/MEMORY.md
1182 /home/skilland/.hermes/profiles/homelab/memories/USER.md
6087 total
```

Comando:

```bash
hermes --profile homelab prompt-size
```

Resultado resumido:

```text
System prompt total : 22,604 B
skills index        : 147 B
memory              : 2,148 B
user profile        : 1,518 B
stable              : 17,933 B
context             : 937 B
volatile            : 3,730 B
Tool schemas        : 53,496 B
```

Comando:

```bash
hermes --profile homelab profile show homelab
```

Resultado:

```text
Profile: homelab
Path: /home/skilland/.hermes/profiles/homelab
Model: gpt-5.5 (openai-codex)
Gateway: stopped
Skills: 1
.env: exists
SOUL.md: exists
```

Nota: `Skills: 1` ya estaba presente antes de este cierre. No se creó ninguna skill durante esta run.

## Verificación Gateway / cron / secretos

Comandos:

```bash
pgrep -af "hermes.*gateway" || true
find /home/skilland/.hermes/profiles/homelab/cron -maxdepth 2 -type f -print 2>/dev/null | sort
stat -c '%y %n' /home/skilland/.hermes/profiles/homelab/.env \
  /home/skilland/.hermes/profiles/homelab/auth.json \
  /home/skilland/.hermes/profiles/homelab/config.yaml 2>/dev/null || true
```

Resultado resumido:

- `profile show` mantiene `Gateway: stopped`.
- `pgrep` muestra procesos `tui_gateway.entry` y `tui_gateway.slash_worker` asociados a sesiones Hermes TUI/CLI, no Gateway de mensajería arrancado por esta spec.
- No hay archivos de cron bajo `/home/skilland/.hermes/profiles/homelab/cron`.
- Se verificaron timestamps/rutas de `.env`, `auth.json` y `config.yaml` sin imprimir contenidos.
- No se leyeron ni modificaron secretos.

## Limpieza de artefactos

Se movió el artefacto de auditoría v1.1 fuera de outputs finales:

```text
04_outputs/2026-07-02_hermes_identity_memory_v1_1_audit.md
-> 05_scratch/2026-07-02_hermes_identity_memory_v1_1_audit.md
```

Motivo: era material de análisis/borrador, no output final de cierre.

## Documentación creada

- `04_outputs/2026-07-02_hermes_identity_memory_foundation_close_v1.md`
- `03_runs/2026-07-02_hermes_identity_memory_foundation_close_run_01.md`

## Decisión registrada

Se actualizó `03_specs/decisions.md` con:

```text
2026-07-02: Cerrar 004 tras aplicar y verificar la v1.1 estratégica de identidad/memoria de Hermes `homelab`; `SOUL.md`, `MEMORY.md` y `USER.md` quedan como fundación operativa para pasar a repo real read-only. Status: accepted
```

## Archivo de spec

Acción:

```bash
mv 03_specs/now/004_hermes_identity_memory_foundation.md 03_specs/done/004_hermes_identity_memory_foundation.md
```

Resultado esperado: `03_specs/now/` queda solo con `.keep`.

## Verificación posterior al archivo

Después de mover la spec:

```text
Specs now after close:
03_specs/now/.keep

Spec done exists:
03_specs/done/004_hermes_identity_memory_foundation.md
```

Git status final relevante:

```text
## main...origin/main
 M 02_context/HERMES_PROFILE_FOUNDATION.md
 M 03_specs/decisions.md
 D 03_specs/now/004_hermes_identity_memory_foundation.md
?? 03_runs/2026-07-02_hermes_identity_memory_foundation_close_run_01.md
?? 03_runs/2026-07-02_hermes_identity_memory_v1_1_run_01.md
?? 03_specs/done/004_hermes_identity_memory_foundation.md
?? 04_outputs/2026-07-02_hermes_identity_memory_foundation_close_v1.md
```

También quedan artefactos no creados por este cierre y/o de runs previas: `.hermes/`, `04_outputs/2026-07-02_punto_situacion_homelab_v1.md`, `05_scratch/2026-07-02_004_hermes_identity_memory_v1_1_implementation_spec.md`, `05_scratch/2026-07-02_hermes_identity_memory_v1_1_audit.md`, `05_scratch/hermes_identity_memory_v1_1_before/`.

## No alcance

- No se rediseñó identidad.
- No se hizo diagnóstico estratégico nuevo.
- No se creó una spec nueva.
- No se hizo commit.
- No se modificó `.env`.
- No se leyó ni modificó `auth.json`.
- No se editó `config.yaml`.
- No se tocaron secretos ni tokens.
- No se arrancó Gateway de mensajería.
- No se conectó Telegram, WhatsApp, Gmail, Drive, CRM, Slack ni Discord.
- No se configuraron webhooks.
- No se configuraron MCPs externos.
- No se creó cron job.
- No se instaló browser, Playwright, Chrome ni servicios.
- No se creó skill nueva.
- No se tocó producción ni clientes.
- No se enviaron mensajes reales.

## Riesgos

- `homelab` corre con permisos reales del usuario `skilland`; no es sandbox de filesystem.
- El perfil está en modo baja fricción: `approvals.mode: false`, `memory.write_approval: false`, `skills.write_approval: false`.
- `config.yaml` sigue con aviso de versión pendiente (`0 → 32`).
- `prompt-size` muestra `user profile: 1,518 B`; archivo real bajo límite, pero margen bajo.
- Procesos `tui_gateway.*` siguen pudiendo confundirse con Gateway real.
- Existe `Skills: 1` en el perfil al cierre, previo a esta tarea.

## Veredicto

Pasa.

004 queda cerrada formalmente y archivada. Recomiendo abrir 005 como `005_hermes_first_real_repo_readonly_operator`.
