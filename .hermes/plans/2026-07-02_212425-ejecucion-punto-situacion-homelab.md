# Ejecución Paso A Paso Del Punto De Situación HomeLab Implementation Plan

> **For Hermes:** Use subagent-driven-development skill to implement this plan task-by-task.

**Goal:** Convertir el punto de situación del HomeLab en una secuencia segura de microtareas ejecutables por otra sesión de Hermes, con esta sesión actuando como planificador/evaluador.

**Architecture:** Separar roles: esta sesión mantiene criterio, secuencia, prompts de handoff y evaluación; la otra sesión Hermes ejecuta tareas pequeñas dentro del repo. Primero se cierra el desorden documental de 004; después se actualiza contexto/runtime; solo entonces se crea la spec 005 para operar un repo real en modo read-only.

**Tech Stack:** Markdown repo harness, Hermes CLI perfil `homelab`, git, herramientas de lectura/escritura de archivos, specs en `03_specs/`, contexto en `02_context/`, outputs en `04_outputs/`, run notes en `03_runs/`.

---

## Modo de trabajo recomendado

Raúl abre otra sesión de Hermes para ejecución. Esta sesión queda como planificador/evaluador.

### Rol de esta sesión: planificador/evaluador

Responsabilidades:

- Convertir cada bloque en un prompt claro para la sesión ejecutora.
- Revisar el diff/resultados después de cada bloque.
- Decidir si se puede pasar al siguiente bloque.
- Mantener el orden de una sola spec activa.
- Frenar si Hermes ejecutor intenta conectar externos, tocar secretos o saltar a arquitectura prematura.

### Rol de la otra sesión Hermes: ejecutor

Responsabilidades:

- Ejecutar solo el bloque que Raúl le pase.
- Leer contexto antes de editar.
- Editar archivos concretos.
- Verificar con comandos reales.
- Devolver resumen, archivos tocados, comandos ejecutados, riesgos y preguntas.

### Regla clave

No pedirle a Hermes ejecutor “ordena todo el proyecto”. Pedirle una sola subcosa por vez.

---

## Secuencia general

1. Cierre formal de spec 004.
2. Actualización de runtime notes por drift real.
3. Actualización de `HERMES_PROFILE_FOUNDATION.md`.
4. Limpieza de backlog.
5. Decisión de repo candidato para 005.
6. Creación de spec 005.
7. Evaluación de la spec 005 antes de ejecución.
8. Ejecución posterior de 005 en una nueva tanda, si Raúl aprueba.

---

### Task 1: Cerrar formalmente la spec 004

**Objective:** Sacar `004_hermes_identity_memory_foundation.md` de `03_specs/now/` y archivarla en `03_specs/done/`, dejando `now/` limpio salvo `.keep`.

**Files:**
- Move: `03_specs/now/004_hermes_identity_memory_foundation.md` -> `03_specs/done/004_hermes_identity_memory_foundation.md`
- Verify: `03_specs/now/.keep`

**Step 1: Preflight read-only**

Run:

```bash
pwd
git status --short --branch
find 03_specs/now 03_specs/done -maxdepth 1 -type f -print | sort
```

Expected:

- Repo: `/home/skilland/workspaces/skilland-agentic-homelab`.
- `03_specs/now/004_hermes_identity_memory_foundation.md` exists.
- `03_specs/done/004_hermes_identity_memory_foundation.md` does not already exist.

**Step 2: Move file**

Run:

```bash
mv 03_specs/now/004_hermes_identity_memory_foundation.md 03_specs/done/004_hermes_identity_memory_foundation.md
```

**Step 3: Verify**

Run:

```bash
find 03_specs/now 03_specs/done -maxdepth 1 -type f -print | sort
git status --short
```

Expected:

- `03_specs/now/` contains only `.keep`.
- `03_specs/done/004_hermes_identity_memory_foundation.md` exists.
- Git shows a rename/move or delete+add for spec 004.

**Prompt para Hermes ejecutor:**

```text
Lee AGENTS.md, 01_harness/RULES.md, 01_harness/STACK.md, 01_harness/TASKFLOW.md y 04_outputs/2026-07-02_punto_situacion_homelab_v1.md. Ejecuta solo esta tarea: cerrar formalmente la spec 004 moviendo 03_specs/now/004_hermes_identity_memory_foundation.md a 03_specs/done/004_hermes_identity_memory_foundation.md. No edites otros archivos. Verifica con find y git status. Devuélveme comandos ejecutados, resultado y riesgos.
```

**Evaluation gate:**

Esta sesión debe comprobar:

```bash
find 03_specs/now 03_specs/done -maxdepth 1 -type f -print | sort
git diff --stat
git diff -- 03_specs/now 03_specs/done | sed -n '1,120p'
```

Pass si `now/` queda limpio salvo `.keep` y no hay ediciones de contenido inesperadas.

---

### Task 2: Actualizar `HERMES_RUNTIME_NOTES.md` con estado real actual

**Objective:** Documentar el drift real observado: modelo `gpt-5.5`, `Gateway: stopped`, `Skills: 1`, skill `homelab-microhito-roadmapping`, prompt-size actual y ausencia de canales externos.

**Files:**
- Modify: `02_context/HERMES_RUNTIME_NOTES.md`

**Step 1: Gather current runtime evidence**

Run:

```bash
hermes --profile homelab profile show homelab
hermes --profile homelab prompt-size
find /home/skilland/.hermes/profiles/homelab/skills -maxdepth 4 -name SKILL.md -print | sort
pgrep -af "hermes.*gateway" || true
```

Do not print `.env`, `auth.json`, tokens or secrets.

**Step 2: Add dated section**

Append a section similar to:

```md
## Actualización 2026-07-02: drift real tras punto de situación

Estado verificado:

- Perfil: `homelab`.
- Modelo actual: `gpt-5.5 (openai-codex)`.
- `Gateway: stopped` según `profile show`.
- `Skills: 1` según `profile show`.
- Skill presente: `homelab-microhito-roadmapping`.
- `prompt-size` actual:
  - system prompt total: `20,483 B`
  - skills index: `147 B`
  - memory: `1,671 B`
  - user profile: `1,290 B`
- No se verificó ningún canal externo conectado en esta actualización.
- No se inspeccionaron secretos, `.env` ni `auth.json`.

Nota: esta sección corrige el estado operativo posterior al cierre documentado de la spec 004, donde constaban `gpt-5.4` y `Skills: 0`.
```

If live command values differ, use live values.

**Step 3: Verify diff**

Run:

```bash
git diff -- 02_context/HERMES_RUNTIME_NOTES.md
```

Expected:

- Only a concise dated section added.
- No secrets.
- No rewrite of the whole file.

**Prompt para Hermes ejecutor:**

```text
Ejecuta solo esta tarea: actualizar 02_context/HERMES_RUNTIME_NOTES.md con una sección fechada sobre el estado real actual del perfil homelab. Primero verifica con hermes --profile homelab profile show homelab, hermes --profile homelab prompt-size y búsqueda de SKILL.md en el perfil. No leas ni imprimas .env, auth.json, tokens ni secretos. Añade una sección breve, no reescribas todo el archivo. Devuelve diff y comandos ejecutados.
```

**Evaluation gate:**

Pass si:

- La sección es breve.
- Refleja valores reales.
- No contiene secretos.
- No contradice secciones anteriores sin explicar que son estado histórico.

---

### Task 3: Actualizar `HERMES_PROFILE_FOUNDATION.md`

**Objective:** Corregir el resumen de fundación para que no diga que el perfil tiene `Skills: 0` si ahora tiene una skill aceptable.

**Files:**
- Modify: `02_context/HERMES_PROFILE_FOUNDATION.md`

**Step 1: Read current file**

Run/read:

```bash
sed -n '1,180p' 02_context/HERMES_PROFILE_FOUNDATION.md
```

Equivalent with file read tool is fine.

**Step 2: Patch state section**

Change the current state from:

```md
- `Skills: 0` según `profile show`.
```

to something like:

```md
- `Skills: 1` según `profile show` verificado el 2026-07-02.
- Skill presente: `homelab-microhito-roadmapping`, usada para planificar/criti­car microhitos HomeLab sin abrir canales externos ni arquitectura prematura.
```

Also adjust the limitation line that says an auto-skill was removed so it remains historically true:

```md
- En el cierre de la spec 004 se retiró una auto-skill transitoria y el perfil volvió a `Skills: 0`; posteriormente quedó instalada/aceptada la skill `homelab-microhito-roadmapping`.
```

**Step 3: Verify**

Run:

```bash
git diff -- 02_context/HERMES_PROFILE_FOUNDATION.md
```

Expected: small targeted change.

**Prompt para Hermes ejecutor:**

```text
Ejecuta solo esta tarea: actualizar 02_context/HERMES_PROFILE_FOUNDATION.md para reflejar que hoy el perfil homelab tiene Skills: 1 y la skill homelab-microhito-roadmapping. Mantén la historia de que durante la spec 004 se retiró una auto-skill transitoria, pero aclara el estado posterior. No edites otros archivos. Devuelve diff.
```

**Evaluation gate:**

Pass si el archivo queda consumible en menos de 5 minutos y ya no afirma como estado actual algo falso.

---

### Task 4: Limpiar `03_specs/backlog.md`

**Objective:** Separar items ya completados de pendientes reales para que el siguiente agente no reabra trabajo viejo.

**Files:**
- Modify: `03_specs/backlog.md`

**Step 1: Read current backlog and done specs**

Run:

```bash
cat 03_specs/backlog.md
find 03_specs/done -maxdepth 1 -type f -print | sort
```

Equivalent read/search tools are fine.

**Step 2: Rewrite backlog concisely**

Target structure:

```md
# BACKLOG

One line per item.

## Hecho / absorbido por microhitos anteriores

- [x] Escribir spec inicial de Hermes Deep Research / Hermes Literacy.
- [x] Reunir y rankear fuentes oficiales/comunitarias de Hermes.
- [x] Inspeccionar estado real inicial del VPS/runtime durante instalación Hermes.
- [x] Definir formato operativo de run notes mediante `03_runs/`.
- [x] Configurar fundación de identidad/memoria del perfil Hermes `homelab`.

## Pendiente

- [ ] Cerrar formalmente spec 004 en `03_specs/done/` si aún aparece en `03_specs/now/`.
- [ ] Decidir el primer repo real de bajo riesgo para `005_hermes_first_real_repo_readonly_operator`.
- [ ] Crear spec 005 para lectura read-only de un repo real por Hermes.
- [ ] Definir checklist de aprobación para acciones externas/sensibles antes de Gateway, Telegram, WhatsApp, Gmail, Drive, CRM o webhooks.
- [ ] Decidir si mantener `homelab` en baja fricción o crear un perfil desechable para pruebas agresivas.
- [ ] Evaluar si conviene resolver migración de config `v0 -> v30` antes de loops largos.
```

If Task 1 is already done by then, mark the first pending item as done or omit it.

**Step 3: Verify**

Run:

```bash
git diff -- 03_specs/backlog.md
```

Expected: no raw dumps, no stale duplicated items.

**Prompt para Hermes ejecutor:**

```text
Ejecuta solo esta tarea: limpiar 03_specs/backlog.md a partir del punto de situación y specs done. Separa items hechos/absorbidos por microhitos anteriores de pendientes reales. Mantén formato corto, una línea por item. No abras spec 005 todavía. Devuelve diff y explica qué items consideraste absorbidos.
```

**Evaluation gate:**

Pass si el backlog ya no invita a repetir tareas completadas y deja claro qué falta antes de 005.

---

### Task 5: Elegir repo candidato para 005

**Objective:** Tomar una decisión de foco antes de escribir spec 005.

**Files:**
- No files initially.
- Optional later: `03_specs/decisions.md` if Raúl confirms.

**Step 1: Candidate list**

Known candidates from context:

- `RaulAM7/google-workspace-CLI-Experiment`
- `RaulAM7/funnel-and-offer-academy`
- another low-risk internal repo selected by Raúl

Avoid as first target:

- `Skilland-ai/skilland-crm`
- production systems
- repos with client data/secrets

**Step 2: Ask Raúl for decision**

Recommended wording:

```text
Para 005 necesitamos elegir un repo real de bajo riesgo. Mi recomendación es empezar por el más legible y menos sensible. Opciones: Google Workspace CLI Experiment, Funnel and Offer Academy u otro repo interno. No recomiendo CRM todavía. ¿Cuál elegimos?
```

**Step 3: Record decision after Raúl answers**

If Raúl chooses, add to `03_specs/decisions.md`:

```md
- 2026-07-02: Usar `<repo>` como primer repo real de bajo riesgo para `005_hermes_first_real_repo_readonly_operator`. Status: accepted
```

**Prompt para Hermes ejecutor:**

Do not delegate this before Raúl chooses. This is a human decision gate.

**Evaluation gate:**

Pass only when Raúl names the repo or explicitly delegates the choice.

---

### Task 6: Crear spec 005

**Objective:** Crear una spec ejecutable para que Hermes lea un repo real en modo read-only y produzca una síntesis operativa útil sin tocar externos ni producción.

**Files:**
- Create: `03_specs/now/005_hermes_first_real_repo_readonly_operator.md`
- Maybe modify: `03_specs/decisions.md` if not already updated

**Precondition:**

- `03_specs/now/` contains only `.keep`.
- Repo candidato elegido.
- Runtime/context notes updated.

**Step 1: Verify spec discipline**

Run:

```bash
find 03_specs/now -maxdepth 1 -type f -print | sort
```

Expected:

```text
03_specs/now/.keep
```

**Step 2: Draft spec 005**

Suggested structure:

```md
# 005 Hermes First Real Repo Readonly Operator

Fecha: 2026-07-02

## Resultado

Hermes `homelab` lee un repo real de bajo riesgo en modo read-only y produce una síntesis operativa útil para decidir el primer microhito real de ese repo.

## Resumen en cristiano

Hasta ahora HomeLab ha probado Hermes sobre sí mismo. Este microhito comprueba si Hermes puede aportar criterio sobre un repo real sin escribir, conectar canales ni tocar producción.

## Repo objetivo

- Repo: `<repo elegido>`
- Ruta local esperada: `Unknown` hasta verificar.
- Sensibilidad: bajo riesgo, sin producción ni secretos.

## Objetivo

1. Verificar que el repo existe localmente o documentar si falta.
2. Leer solo archivos seguros: README, AGENTS/CLAUDE si existen, estructura, specs/docs públicas del repo.
3. Producir síntesis operativa en `04_outputs/` del HomeLab.
4. Proponer el primer microhito útil para ese repo.
5. No escribir dentro del repo objetivo.

## No objetivos

- No modificar el repo objetivo.
- No conectar Gmail, Drive, CRM, WhatsApp, Telegram, Slack, Discord ni webhooks.
- No leer `.env`, `auth.json`, tokens, credenciales ni secretos.
- No ejecutar comandos destructivos.
- No abrir PRs.
- No instalar dependencias salvo aprobación explícita.

## Archivos a leer primero

1. `AGENTS.md`
2. `01_harness/RULES.md`
3. `01_harness/STACK.md`
4. `01_harness/TASKFLOW.md`
5. `02_context/HERMES_PROFILE_FOUNDATION.md`
6. `02_context/HERMES_RUNTIME_NOTES.md`
7. `04_outputs/2026-07-02_punto_situacion_homelab_v1.md`
8. Esta spec activa

## Plan de ejecución

### 1. Preflight HomeLab

Run:

```bash
pwd
git status --short --branch
find 03_specs/now -maxdepth 1 -type f -print | sort
hermes --profile homelab profile show homelab
```

### 2. Localizar repo objetivo

Run safe read-only discovery under `/home/skilland/workspaces`.

### 3. Inventario read-only del repo objetivo

Read only:

- README
- AGENTS/CLAUDE/context files if present
- project manifest if present
- docs/specs relevant files

Do not read secret files.

### 4. Pedir a Hermes una síntesis operativa

Hermes should answer:

- Qué es el repo.
- Qué señales de madurez tiene.
- Qué riesgos tiene.
- Qué primer microhito útil recomienda.
- Qué no debe tocar todavía.

### 5. Crear output HomeLab

Create:

`04_outputs/2026-07-02_hermes_first_real_repo_readonly_operator_v1.md`

### 6. Crear run note

Create:

`03_runs/2026-07-02_hermes_first_real_repo_readonly_operator_run_01.md`

## Criterios de aceptación

- Spec 005 es la única activa en `03_specs/now/`.
- Se eligió repo real de bajo riesgo.
- No se modificó el repo objetivo.
- No se leyeron ni imprimieron secretos.
- No se conectaron sistemas externos.
- Gateway sigue parado.
- Existe output en `04_outputs/`.
- Existe run note en `03_runs/`.
- La síntesis propone un primer microhito útil y pequeño.
- Todo output generado está en español.

## Riesgos

- El perfil `homelab` está en baja fricción.
- Hermes no sandboxea filesystem.
- Un repo real puede contener secretos; hay que evitarlos explícitamente.
- La lectura puede quedarse superficial si el repo no tiene buen README/contexto.

## Siguiente acción recomendada

Si 005 pasa, convertir el microhito propuesto en la spec 006, todavía sin canales externos.
```

**Step 3: Verify spec**

Run:

```bash
git diff -- 03_specs/now/005_hermes_first_real_repo_readonly_operator.md 03_specs/decisions.md
```

**Prompt para Hermes ejecutor:**

```text
Ejecuta solo esta tarea: crear la spec 005 para que Hermes lea un repo real de bajo riesgo en modo read-only. Preconditions: 03_specs/now debe estar limpio salvo .keep y el repo elegido por Raúl es <REPO>. No ejecutes la spec. Solo escribe 03_specs/now/005_hermes_first_real_repo_readonly_operator.md y, si procede, añade una decisión breve en 03_specs/decisions.md. La spec debe estar en español, con objetivo, no objetivos, archivos a leer, plan, criterios de aceptación, riesgos y siguiente acción. No conectes externos ni toques el repo objetivo.
```

**Evaluation gate:**

Pass si:

- La spec no ejecuta nada todavía.
- Tiene límites read-only explícitos.
- Incluye no tocar secretos.
- Incluye outputs y run note.
- Mantiene una sola spec activa.

---

### Task 7: Evaluación global antes de ejecutar 005

**Objective:** Revisar que el cierre administrativo está correcto antes de dejar a Hermes ejecutar la lectura read-only.

**Files:**
- No edits.

**Step 1: Verify repo state**

Run:

```bash
git status --short --branch
find 03_specs/now 03_specs/done -maxdepth 1 -type f -print | sort
```

Expected:

- Only `005_hermes_first_real_repo_readonly_operator.md` active in `now/` plus `.keep`.
- 004 archived in `done/`.

**Step 2: Verify updated docs**

Check:

- `02_context/HERMES_RUNTIME_NOTES.md` has 2026-07-02 update.
- `02_context/HERMES_PROFILE_FOUNDATION.md` mentions `Skills: 1` or historical/current split.
- `03_specs/backlog.md` no longer has stale items as pending.

**Step 3: Decide commit or not**

By default, do not commit unless Raúl asks.

Suggested status to Raúl:

```text
Cierre administrativo listo. La spec 005 está preparada pero no ejecutada. Si quieres, ahora abres Hermes ejecutor y le pasas el prompt de ejecución de 005.
```

---

## Orden recomendado de sesiones

### Sesión A: esta sesión

- Planifica.
- Entrega prompts.
- Evalúa resultados.
- No ejecuta tareas del repo salvo planes/documentos de planificación.

### Sesión B: Hermes ejecutor

Ejecuta en este orden:

1. Task 1.
2. Vuelve con resultado.
3. Espera evaluación.
4. Task 2.
5. Vuelve con resultado.
6. Espera evaluación.
7. Task 3.
8. Vuelve con resultado.
9. Espera evaluación.
10. Task 4.
11. Vuelve con resultado.
12. Espera decisión humana para Task 5.
13. Task 6 solo cuando Raúl elija repo.

---

## Primera instrucción concreta para Raúl

Abrir otra sesión de Hermes en el repo HomeLab y pegar este prompt:

```text
Lee AGENTS.md, 01_harness/RULES.md, 01_harness/STACK.md, 01_harness/TASKFLOW.md y 04_outputs/2026-07-02_punto_situacion_homelab_v1.md. Ejecuta solo esta tarea: cerrar formalmente la spec 004 moviendo 03_specs/now/004_hermes_identity_memory_foundation.md a 03_specs/done/004_hermes_identity_memory_foundation.md. No edites otros archivos. Verifica con find y git status. Devuélveme comandos ejecutados, resultado y riesgos.
```

Cuando Hermes ejecutor responda, pegar aquí su salida para evaluación antes de pasar a la Task 2.

---

## Riesgos y mitigaciones

- **Hermes ejecutor hace demasiado:** prompts de una tarea, archivos exactos, “no edites otros archivos”.
- **Modo baja fricción:** no pedir acciones amplias; usar read-only cuando corresponda.
- **Desorden de specs:** comprobar `03_specs/now/` antes de crear 005.
- **Secretos:** repetir en cada prompt que no lea `.env`, `auth.json`, tokens ni credenciales.
- **Canales externos:** mantener Gateway, Telegram, WhatsApp, Gmail, Drive, CRM, Slack, Discord, webhooks y MCPs fuera del alcance.

## Open questions

- ¿Qué repo elegirá Raúl para 005?
- ¿Se acepta oficialmente la skill `homelab-microhito-roadmapping` como parte del perfil `homelab`?
- ¿Conviene mantener `homelab` en baja fricción o crear un perfil desechable para pruebas agresivas?
- ¿Hay que resolver migración config `v0 -> v30` antes de loops largos?
