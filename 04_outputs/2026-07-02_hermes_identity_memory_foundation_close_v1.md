# Cierre formal 004 — Hermes identity/memory foundation

Fecha: 2026-07-02

## Resumen en cristiano

La spec 004 queda lista para cierre formal.

Hermes `homelab` ya no opera como asistente genérico: tiene una identidad v1.1 más estratégica en `SOUL.md`, memoria durable compacta en `MEMORY.md` y perfil de Raúl actualizado en `USER.md`. La v1.1 refuerza North Star, producto antes que arquitectura, aprendizaje transferible, repos como fábricas/departamentos y la preferencia de Raúl por brainstorming/validación antes de prompts ejecutivos en decisiones estratégicas.

No se abrió ninguna integración externa ni se tocaron secretos. El siguiente paso recomendado ya no es seguir retocando identidad: es probar Hermes sobre un repo real en modo read-only y producir una utilidad pequeña, reversible y documentada.

## Evidencia usada

- Spec activa ejecutada: `03_specs/now/004_hermes_identity_memory_foundation.md`.
- Run fundacional: `03_runs/2026-06-21_hermes_identity_memory_foundation_run_01.md`.
- Run v1.1: `03_runs/2026-07-02_hermes_identity_memory_v1_1_run_01.md`.
- Output fundacional: `04_outputs/2026-06-21_hermes_identity_memory_foundation_v1.md`.
- Contexto actualizado: `02_context/HERMES_PROFILE_FOUNDATION.md`.
- Runtime notes: `02_context/HERMES_RUNTIME_NOTES.md`.

## Estado final del perfil Hermes `homelab`

Archivos persistentes verificados:

```text
3091 /home/skilland/.hermes/profiles/homelab/SOUL.md
1814 /home/skilland/.hermes/profiles/homelab/memories/MEMORY.md
1182 /home/skilland/.hermes/profiles/homelab/memories/USER.md
6087 total
```

`prompt-size` final:

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

Estado del perfil:

```text
Profile: homelab
Path: /home/skilland/.hermes/profiles/homelab
Model: gpt-5.5 (openai-codex)
Gateway: stopped
Skills: 1
.env: exists
SOUL.md: exists
```

Nota: `Skills: 1` ya estaba presente al inicio del cierre; no se creó ninguna skill durante esta tarea.

## QA final contra 004

- [x] `SOUL.md` existe y contiene identidad HomeLab no genérica.
- [x] `MEMORY.md` existe en el perfil `homelab`.
- [x] `USER.md` existe en el perfil `homelab`.
- [x] `MEMORY.md` queda bajo el límite aproximado de `2200 B` como archivo real: `1814 B`.
- [x] `USER.md` queda bajo el límite aproximado de `1375 B` como archivo real: `1182 B`.
- [x] `prompt-size` muestra `memory` y `user profile` mayores que `0 B`.
- [x] Tests de sesión nueva de la v1.1 pasaron: identidad/North Star, decisión estratégica no validada, restricción ante WhatsApp/Gmail y Gateway no arrancado.
- [x] `02_context/HERMES_PROFILE_FOUNDATION.md` refleja la actualización v1.1.
- [x] Existe run note de aplicación v1.1.
- [x] Existe output fundacional humano.
- [x] Se creó este output final de cierre.
- [x] La spec 004 puede archivarse en `03_specs/done/`.

## No alcance verificado

Durante el cierre formal:

- No se rediseñó identidad.
- No se abrió diagnóstico estratégico nuevo.
- No se creó spec nueva.
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

El comando `pgrep -af "hermes.*gateway"` sigue mostrando procesos `tui_gateway.entry` y `tui_gateway.slash_worker` de sesiones Hermes TUI/CLI, pero `profile show` mantiene `Gateway: stopped`; no hay evidencia de Gateway de mensajería arrancado por esta spec.

## Limpieza de artefactos

Artefacto de auditoría v1.1 movido fuera de outputs finales:

```text
04_outputs/2026-07-02_hermes_identity_memory_v1_1_audit.md
-> 05_scratch/2026-07-02_hermes_identity_memory_v1_1_audit.md
```

Motivo: era material de análisis/borrador, no output final de cierre.

## Estado final de specs

La spec 004 se archiva en:

```text
03_specs/done/004_hermes_identity_memory_foundation.md
```

`03_specs/now/` queda libre para el siguiente microhito, solo con `.keep`.

## Riesgos que quedan

- `homelab` corre con permisos reales del usuario `skilland`; el perfil Hermes no sandboxea filesystem.
- El perfil sigue en modo de baja fricción: `approvals.mode: false`, `memory.write_approval: false`, `skills.write_approval: false`.
- `config.yaml` sigue con aviso de versión pendiente (`0 → 32`).
- `prompt-size` muestra `user profile: 1,518 B`; el archivo `USER.md` está bajo límite, pero conviene no expandirlo mucho más.
- Los procesos `tui_gateway.*` pueden confundirse con Gateway real; hay que seguir usando `profile show` y comandos específicos para distinguirlos.
- Hay una skill existente en el perfil (`Skills: 1`) previa a este cierre; no forma parte de 004 y no fue modificada.

## Recomendación de siguiente microhito

Recomiendo abrir:

```text
005_hermes_first_real_repo_readonly_operator
```

Objetivo recomendado:

- Elegir un repo real de bajo riesgo.
- Hacer que Hermes lo lea en modo read-only.
- Producir una síntesis operativa útil.
- Proponer un primer microhito pequeño y reversible.
- No conectar externos, no tocar producción y no crear automatizaciones todavía.

## Veredicto

Pasa.

La spec 004 queda cerrada formalmente tras la v1.1 estratégica de identidad/memoria.
