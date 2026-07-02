# Punto de situación HomeLab v1

Fecha: 2026-07-02

## Resumen en cristiano

HomeLab ya no está en fase cero. El repo tiene contexto base, specs ejecutadas y Hermes instalado en el VPS. El foco real ha sido ganar intimidad con Hermes antes de conectar canales externos o automatizar nada sensible.

El avance principal: Hermes `homelab` ya existe como perfil operativo, tiene identidad propia, memoria base y perfil de usuario. Ya no debería comportarse como asistente genérico. También hay una primera skill en el perfil `homelab` para pensar roadmaps/microhitos del HomeLab.

La fricción actual no es técnica dura: es de orden. La spec 004 parece ejecutada y validada, pero sigue en `03_specs/now/`. Antes de abrir el siguiente microhito conviene cerrar formalmente esa spec y dejar el repo en estado limpio.

## Dónde estamos

### Completado

1. **Contexto inicial del HomeLab**
   - `02_context/` contiene brief, facts, constraints, glossary y links.
   - El repo ya se entiende como laboratorio interno rompible de Skilland/Reboot sobre el VPS real.
   - North Star queda como brújula estratégica; HomeLab como bajada experimental.

2. **Hermes Deep Research / Hermes Literacy**
   - Spec archivada: `03_specs/done/001_hermes_deep_research.md`.
   - Output principal: `04_outputs/2026-06-21_hermes_metagame_initial_synthesis.md`.
   - Aprendizaje: Hermes no es “otro chat”; es runtime con perfiles, memoria, skills, cron, gateway, kanban, dashboard, MCP/API/ACP, etc.

3. **Hermes Intimacy: instalación y smoke test**
   - Spec archivada: `03_specs/done/002_hermes_intimacy_install_smoke_test.md`.
   - Output principal: `04_outputs/2026-06-21_hermes_intimacy_install_smoke_test_v1.md`.
   - Hermes quedó instalado en el VPS como usuario `skilland`.
   - Binario: `/home/skilland/.local/bin/hermes`.
   - Perfil `homelab`: `/home/skilland/.hermes/profiles/homelab`.
   - Gateway quedó parado.
   - No se conectaron canales externos.

4. **Onboarding operativo de Raúl con Hermes**
   - Spec archivada: `03_specs/done/003_hermes_self_guided_operator_onboarding.md`.
   - Output principal: `04_outputs/2026-06-21_hermes_self_guided_operator_onboarding_v1.md`.
   - Raúl practicó abrir, inspeccionar, usar y retomar Hermes con el perfil `homelab`.
   - Se aprendió que Hermes puede instruir su propio uso si el prompt es paso a paso y con límites claros.
   - Por decisión de Raúl, el perfil quedó en modo baja fricción:
     - `approvals.mode: false`
     - `memory.write_approval: false`
     - `skills.write_approval: false`

5. **Fundación de identidad y memoria de Hermes**
   - Spec activa en carpeta `now`: `03_specs/now/004_hermes_identity_memory_foundation.md`.
   - Run note: `03_runs/2026-06-21_hermes_identity_memory_foundation_run_01.md`.
   - Output principal: `04_outputs/2026-06-21_hermes_identity_memory_foundation_v1.md`.
   - QA documentada como pasada.
   - `SOUL.md` dejó de ser genérico.
   - Existen `MEMORY.md` y `USER.md` en el perfil `homelab`.
   - Hermes pasó tests de identidad, partición conceptual, restricción ante WhatsApp y relación North Star → HomeLab → Divi-DClick → productización.

## Estado real verificado hoy

Comando base ejecutado:

```bash
git status --short --branch
```

Resultado relevante:

```text
## main...origin/main
```

No hay cambios locales visibles en el repo en este momento.

Estado de specs:

```text
03_specs/done/001_hermes_deep_research.md
03_specs/done/002_hermes_intimacy_install_smoke_test.md
03_specs/done/003_hermes_self_guided_operator_onboarding.md
03_specs/now/.keep
03_specs/now/004_hermes_identity_memory_foundation.md
```

Lectura: 001, 002 y 003 están archivadas. La 004 sigue en `now`, aunque su run note dice `Veredicto: pasa`. Eso es el principal descuadre de orden.

Estado actual del perfil `homelab`:

```text
Profile: homelab
Path:    /home/skilland/.hermes/profiles/homelab
Model:   gpt-5.5 (openai-codex)
Gateway: stopped
Skills:  1
.env:    exists
SOUL.md: exists
Alias:   homelab → hermes -p homelab
```

Prompt-size actual:

```text
System prompt total : 20,483 B
skills index        : 147 B
memory              : 1,671 B
user profile        : 1,290 B
```

Diferencias frente al cierre documentado de la spec 004:

- Antes se documentó modelo `gpt-5.4`; hoy el perfil muestra `gpt-5.5`.
- Antes se documentó `Skills: 0`; hoy el perfil muestra `Skills: 1`.
- La skill existente es:
  - `/home/skilland/.hermes/profiles/homelab/skills/homelab/homelab-microhito-roadmapping/SKILL.md`
- Esa skill no parece peligrosa: sirve para planificar y criticar roadmaps de microhitos HomeLab, en español, evitando arquitectura prematura y canales externos antes de tiempo.

## Qué está bien

- La base conceptual está clara: North Star → HomeLab → Hermes/Codex → aprendizajes transferibles.
- El repo ya tiene harness mínimo y trazabilidad: specs, run notes, outputs, decisiones y contexto.
- Hermes ya está instalado y probado localmente.
- El perfil `homelab` tiene identidad y memoria funcionales.
- No se han conectado Telegram, WhatsApp, Gmail, Drive, CRM, Slack, Discord, webhooks ni MCPs externos.
- Gateway sigue parado.
- La estrategia de avanzar por microhitos sigue funcionando.

## Qué está desordenado o pendiente

1. **Cerrar formalmente la spec 004**
   - Está ejecutada y QA pasó, pero sigue en `03_specs/now/`.
   - Acción recomendada: moverla a `03_specs/done/004_hermes_identity_memory_foundation.md`.

2. **Actualizar el punto runtime por drift real**
   - `HERMES_RUNTIME_NOTES.md` aún documenta el cierre de 004 con `gpt-5.4` y `Skills: 0`.
   - Hoy el perfil muestra `gpt-5.5` y `Skills: 1`.
   - Acción recomendada: añadir una sección fechada, no reescribir todo.

3. **Decidir si la skill `homelab-microhito-roadmapping` queda aceptada**
   - Parece útil y alineada.
   - Pero conviene registrarla como estado real del perfil, porque rompe la afirmación anterior de “Skills: 0”.

4. **Resolver o aceptar la configuración de baja fricción**
   - `approvals.mode: false`, `memory.write_approval: false`, `skills.write_approval: false` aceleran mucho.
   - Riesgo: Hermes puede escribir memoria/skills sin staging si se lo permitimos en una sesión.
   - Recomendación: mantenerlo solo si el siguiente microhito tiene límites claros y read-only cuando toque.

5. **Actualizar backlog**
   - `03_specs/backlog.md` todavía contiene items antiguos, algunos ya superados por los microhitos 001-004.
   - Conviene limpiar backlog antes de abrir 005.

## Riesgos actuales

- **Riesgo de falsa seguridad:** el perfil Hermes no es sandbox de filesystem. Corre como usuario `skilland`.
- **Riesgo de auto-escritura:** baja fricción + skills/memoria escribibles puede generar cambios inesperados si no se acota el prompt.
- **Riesgo de saltar etapas:** la tentación natural es pasar ya a Telegram, WhatsApp, cron o gateway. Todavía no toca.
- **Riesgo de desorden documental:** si 004 no se archiva y runtime notes no se actualiza, el siguiente agente puede interpretar mal el estado real.

## Recomendación de siguiente movimiento

Antes de diseñar 005, hacer un micro-cierre administrativo:

1. Mover `03_specs/now/004_hermes_identity_memory_foundation.md` a `03_specs/done/004_hermes_identity_memory_foundation.md`.
2. Añadir una nota fechada a `02_context/HERMES_RUNTIME_NOTES.md` con:
   - modelo actual `gpt-5.5`;
   - `Gateway: stopped`;
   - `Skills: 1`;
   - skill `homelab-microhito-roadmapping` existente;
   - prompt-size actual;
   - no canales externos conectados.
3. Actualizar `02_context/HERMES_PROFILE_FOUNDATION.md` para que no diga que el perfil tiene `Skills: 0` si ya no es verdad.
4. Limpiar `03_specs/backlog.md` separando lo ya hecho de lo pendiente.
5. Crear la spec 005.

## Siguiente microhito recomendado

Nombre sugerido:

```text
005_hermes_first_real_repo_readonly_operator
```

Objetivo:

- Elegir un repo real de bajo riesgo.
- Pedir a Hermes que lo lea en modo read-only.
- Producir una síntesis operativa útil.
- Proponer un primer microhito real dentro de ese repo.
- No conectar externos.
- No tocar producción.
- No enviar mensajes reales.

Criterio de éxito:

Hermes deja de hablar solo de Hermes y empieza a demostrar utilidad sobre un repo real, pero sin escribir ni conectar nada sensible.

## Decisión que necesita Raúl

La decisión clave ahora no es técnica, es de foco:

```text
¿El siguiente repo de bajo riesgo será Google Workspace CLI Experiment, Funnel and Offer Academy u otro repo interno?
```

Mi recomendación provisional: empezar por el repo más bajo riesgo y más legible, no por CRM ni producción.

## Veredicto

Vamos bien. El HomeLab ya tiene base, Hermes ya está instalado y el perfil `homelab` ya tiene identidad. Ahora toca ordenar el cierre de 004 y pasar de “Hermes sobre Hermes” a “Hermes leyendo un repo real en read-only”.
