# 003 Hermes Self-Guided Operator Onboarding

Fecha: 2026-06-21

## Resultado

Raul aprende a operar Hermes directamente en el CLI con el perfil `homelab`, guiado por Hermes como instructor paso a paso.

Este microhito no es de memoria, skills, cron, gateway ni integraciones. Es una practica controlada para que el humano use Hermes, vea sus respuestas, entienda sus limites y gane criterio operativo antes de pedirle automatismos.

## Archivos A Leer Primero

Leer en este orden antes de escribir o ejecutar:

1. `AGENTS.md`
2. `01_harness/RULES.md`
3. `01_harness/STACK.md`
4. `01_harness/TASKFLOW.md`
5. Todos los archivos de `02_context/`
6. Esta spec activa: `03_specs/now/003_hermes_self_guided_operator_onboarding.md`
7. Run previo: `03_runs/2026-06-21_hermes_intimacy_install_smoke_test_run_01.md`
8. Output previo: `04_outputs/2026-06-21_hermes_intimacy_install_smoke_test_v1.md`

## Objetivo

Pasar de "Hermes instalado y validado" a "Raul sabe pilotar una sesion Hermes basica".

El ejecutor no debe usar Codex para hacer el trabajo pesado. Debe preparar, acompanar y documentar una sesion donde Raul opera Hermes directamente.

## Roles

- Codex arquitecto: disena specs y evalua resultados. No ejecuta esta practica dentro de Hermes.
- Hermes `homelab`: actua como instructor dentro del CLI.
- Raul: ejecuta comandos, lee resultados, decide aprobaciones y copia lo relevante para la run note.
- Sesion ejecutora: guia el cumplimiento de la spec, recopila evidencias y escribe los entregables.

## Alcance

- Abrir Hermes CLI con el perfil `homelab`.
- Pegar un prompt instructor en Hermes.
- Practicar comandos basicos de introspeccion.
- Hacer que Hermes lea contexto local del repo.
- Confirmar limites operativos: no gateway, no canales externos, no webhooks, no MCPs externos, no `--yolo`.
- Practicar cierre, guardado y continuidad de sesion.
- Documentar aprendizajes, fricciones y riesgos.

## Fuera De Alcance

- No activar memoria como funcionalidad de trabajo.
- No aprobar escrituras de memoria salvo que Raul lo pida explicitamente y quede documentado.
- No crear ni aprobar skills.
- No modificar `SOUL.md`, `MEMORY.md`, `USER.md` ni archivos de perfil.
- No arrancar Gateway.
- No configurar cron jobs.
- No configurar webhooks.
- No configurar MCPs externos.
- No conectar Telegram.
- No conectar WhatsApp.
- No conectar Gmail.
- No conectar Drive.
- No conectar CRM.
- No conectar Kapso.
- No conectar Slack.
- No conectar Discord.
- No exponer dashboard o Mission Control publicamente.
- No tocar sistemas productivos.
- No usar `--yolo`.
- No hacer instalacion, migracion o refactor de configuracion salvo diagnostico read-only.

## Estado Inicial Esperado

Segun la spec 002 ya ejecutada:

- Binario: `/home/skilland/.local/bin/hermes`
- Alias: `homelab`
- Perfil: `/home/skilland/.hermes/profiles/homelab`
- Provider: `openai-codex`
- Modelo: `gpt-5.4`
- `terminal.cwd`: `/home/skilland/workspaces/skilland-agentic-homelab`
- `approvals.mode`: `manual`
- `memory.write_approval`: `true`
- `skills.write_approval`: `true`
- Gateway: stopped
- Skills: 0

La sesion ejecutora debe verificar el estado real. Si algo cambio, documentarlo y ajustar solo en modo diagnostico, sin reparar automaticamente.

## Prompt Para Pegar En Hermes

Raul debe abrir Hermes y pegar este prompt:

```text
Actua como instructor de Hermes para Skilland Agentic HomeLab. Guiame paso a paso, en espanol, para aprender a operar esta sesion. No ejecutes trabajo autonomo pesado. Antes de cada accion explicame que vamos a comprobar y por que. No conectes sistemas externos, no arranques gateway, no uses cron, webhooks, MCPs externos ni --yolo. No escribas memoria, skills ni archivos salvo que yo lo apruebe explicitamente. Primero lee AGENTS.md, README.md y la spec activa, y luego guiame por los comandos basicos de inspeccion.
```

Reglas para Raul:

- No pegues secretos, tokens ni credenciales.
- Si Hermes propone escribir archivos, memoria o skills, pausa y decide explicitamente.
- Para esta spec, la respuesta por defecto a escrituras es no.
- Copia a la sesion ejecutora los outputs relevantes, no toda la conversacion si es demasiado larga.

## Plan De Ejecucion

### 1. Preflight Fuera De Hermes

Desde el repo:

```bash
cd /home/skilland/workspaces/skilland-agentic-homelab
git status --short --branch
command -v hermes
command -v homelab || true
hermes --profile homelab profile show homelab
hermes --profile homelab config check
pgrep -af "hermes.*gateway" || true
```

Registrar salidas sanitizadas en la run note.

Si `homelab` no existe pero `hermes -p homelab` funciona, documentar el detalle y usar `hermes -p homelab`.

### 2. Apertura De Hermes Por Raul

Raul abre Hermes manualmente:

```bash
cd /home/skilland/workspaces/skilland-agentic-homelab
homelab
```

Si el alias falla:

```bash
hermes -p homelab
```

No usar `--yolo`.

### 3. Instructor Prompt

Raul pega el prompt instructor de esta spec en Hermes.

Hermes debe:

- responder en espanol;
- explicar que actuara como guia, no como ejecutor autonomo;
- leer `AGENTS.md`, `README.md` y la spec activa;
- resumir que esta permitido y prohibido;
- pedir confirmacion antes de cada bloque practico.

### 4. Comandos Basicos A Practicar

Raul debe practicar al menos 6 de estos comandos dentro de Hermes:

```text
/profile
/status
/model
/tools list
/toolsets
/usage
/memory pending
/skills pending
/save
/title
/quit
/resume
```

Minimo recomendado:

```text
/profile
/status
/model
/tools list
/toolsets
/memory pending
/skills pending
/save
```

Para cada comando, Hermes debe explicar:

- que comprueba;
- que salida esperaba;
- que significa el resultado para HomeLab;
- si hay algun riesgo operativo.

### 5. Lectura Local Read-Only

Pedir a Hermes:

```text
Lee 02_context/HERMES_RUNTIME_NOTES.md sin modificar archivos. Resume en espanol: estado actual de Hermes, riesgos principales, y que no deberiamos activar todavia.
```

Condiciones:

- No debe modificar archivos.
- No debe crear memoria.
- No debe crear skill.
- No debe iniciar gateway.
- No debe usar herramientas externas.

### 6. Practica De Aprobaciones

Preguntar a Hermes:

```text
Si durante una sesion propones escribir memoria, crear una skill o editar un archivo, que me deberias pedir antes de hacerlo? Dame un protocolo breve para aprobar o rechazar.
```

Resultado esperado:

- Hermes explica aprobacion previa.
- Hermes separa memoria, skills y archivos.
- Hermes reconoce que en esta spec la politica por defecto es no escribir.
- Si aparecen items pendientes en `/memory pending` o `/skills pending`, Raul debe inspeccionarlos y rechazarlos o dejarlos pendientes, no aprobar a ciegas.

### 7. Cierre Y Continuidad

Practicar:

```text
/title
/save
/quit
```

Despues, probar continuidad solo si no fuerza efectos no deseados:

```bash
homelab --continue
```

o dentro de Hermes:

```text
/resume
```

Documentar si la continuidad funciono, fallo o quedo pendiente.

## Entregables

Crear:

- `03_runs/2026-06-21_hermes_self_guided_operator_onboarding_run_01.md`
- `04_outputs/2026-06-21_hermes_self_guided_operator_onboarding_v1.md`

Actualizar solo si hubo aprendizaje real y Raul aprueba escritura:

- `02_context/HERMES_RUNTIME_NOTES.md`

No crear dumps completos de conversacion salvo que sean breves y utiles.

## Contenido Esperado De La Run Note

`03_runs/2026-06-21_hermes_self_guided_operator_onboarding_run_01.md` debe incluir:

- objetivo;
- archivos leidos;
- comando usado para abrir Hermes;
- prompt pegado en Hermes;
- slash commands practicados;
- salidas relevantes sanitizadas;
- resumen de lo que Hermes explico;
- aprobaciones aparecidas, si hubo;
- que se rechazo o quedo pendiente;
- fricciones;
- aprendizajes de Raul;
- QA contra criterios de aceptacion;
- riesgos;
- preguntas abiertas;
- siguiente accion recomendada.

## Contenido Esperado Del Output Final

`04_outputs/2026-06-21_hermes_self_guided_operator_onboarding_v1.md` debe ser consumible por Raul e incluir:

- que se practico;
- que entiende Raul ahora sobre operar Hermes;
- comandos utiles y cuando usarlos;
- limites que Hermes reconocio;
- errores o fricciones;
- si Hermes sirve como instructor de si mismo;
- que falta antes de entrar en memoria/skills;
- recomendacion del siguiente microhito.

## Criterios De Aceptacion

- [ ] Existe `03_runs/2026-06-21_hermes_self_guided_operator_onboarding_run_01.md`.
- [ ] Existe `04_outputs/2026-06-21_hermes_self_guided_operator_onboarding_v1.md`.
- [ ] Raul opero Hermes directamente en CLI.
- [ ] Hermes actuo como guia paso a paso, no como ejecutor autonomo.
- [ ] Todo el output escrito queda en espanol.
- [ ] Se practicaron al menos 6 slash commands.
- [ ] Hermes leyo contexto del repo y explico limites correctamente.
- [ ] Se hizo una tarea read-only sobre `02_context/HERMES_RUNTIME_NOTES.md`.
- [ ] No se uso `--yolo`.
- [ ] No se arranco Gateway.
- [ ] No se conectaron canales externos.
- [ ] No se configuraron webhooks.
- [ ] No se configuraron cron jobs.
- [ ] No se configuraron MCPs externos.
- [ ] No se tocaron sistemas productivos.
- [ ] No se aprobaron memorias, skills ni escrituras de archivos a ciegas.
- [ ] Si aparecieron pendientes de memoria o skills, quedaron inspeccionados y rechazados o documentados como pendientes.
- [ ] `00_inbox/hermes_sources.md` queda intacto.
- [ ] La recomendacion del siguiente microhito queda clara.

## Riesgos

- Hermes corre con permisos reales del usuario `skilland`; el CLI no es un sandbox fuerte.
- Raul puede aprobar escrituras por inercia si la sesion no va lenta y paso a paso.
- `homelab --continue` puede reabrir contexto anterior; documentar si aparece ruido.
- Algunos comandos pueden variar por version de Hermes; si un comando falla, documentar salida y usar `/help`.
- La sesion puede generar memoria pendiente aunque no se quiera aprobar; inspeccionar y no aprobar por defecto.

## Open Questions

- ¿Hermes como instructor de si mismo mejora de verdad el aprendizaje de Raul frente a Codex guiando desde fuera?
- ¿Que comandos basicos deben convertirse en una chuleta permanente para HomeLab?
- ¿Conviene que el proximo microhito sea memoria/perfiles/skills o antes una segunda sesion de operacion pura?
- ¿La continuidad de sesion (`/resume` o `--continue`) es suficientemente clara para usarla en trabajo real?

## Siguiente Accion Recomendada

Si esta spec pasa, planificar `004_hermes_profile_memory_skill_lab`: laboratorio controlado de `SOUL.md`, memoria bajo aprobacion y una skill minima, todavia sin gateway, canales externos, webhooks, cron ni MCPs externos.

## Handoff Corto Para La Sesion Ejecutora

```text
Lee AGENTS.md, RULES.md, STACK.md, TASKFLOW.md y la spec activa en 03_specs/now/. Ejecuta la spec 003 usando Hermes como guia para Raul, no como ejecucion autonoma de Codex. Documenta resultados, QA y proxima recomendacion en espanol.
```
