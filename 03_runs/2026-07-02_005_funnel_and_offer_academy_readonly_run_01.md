# Run note — 005 funnel_and_offer_academy_readonly_run_01

- Fecha: 2026-07-02
- Objetivo: ejecutar la spec `03_specs/now/005_hermes_first_real_repo_readonly_operator.md` desde HomeLab para diagnosticar en modo read-only el repo `/home/skilland/workspaces/funnel-and-offer-academy` y dejar criterio accionable en HomeLab.

## Archivos leídos

### HomeLab
- `AGENTS.md`
- `01_harness/RULES.md`
- `01_harness/STACK.md`
- `01_harness/TASKFLOW.md`
- `03_specs/now/005_hermes_first_real_repo_readonly_operator.md`
- `03_specs/decisions.md`
- búsqueda de archivos referenciados por la spec y comprobación de faltantes:
  - `04_outputs/2026-07-02_hermes_identity_memory_foundation_close_v1.md` → no encontrado
  - `03_runs/2026-07-02_hermes_identity_memory_foundation_close_run_01.md` → no encontrado
  - `02_context/HERMES_PROFILE_FOUNDATION.md` → no encontrado
  - `02_context/HERMES_RUNTIME_NOTES.md` → no encontrado

### Funnel Academy
- `/home/skilland/workspaces/funnel-and-offer-academy/AGENTS.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/README.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/CLAUDE.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/01_harness/RULES.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/01_harness/STACK.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/01_harness/TASKFLOW.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/02_context/BRIEF.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/02_context/FACTS.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/02_context/CONSTRAINTS.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/02_context/GLOSSARY.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/02_context/LINKS.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/03_specs/now/001_now.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/03_specs/backlog.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/03_specs/decisions.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/04_outputs/academy/STATE.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/04_outputs/academy/INTERACTION-DESIGN.md`
- `/home/skilland/workspaces/funnel-and-offer-academy/04_outputs/ia-mujeres-funnel/STATE.md`
- inventario de alto nivel de:
  - `/home/skilland/workspaces/funnel-and-offer-academy/shared/skills/`
  - `/home/skilland/workspaces/funnel-and-offer-academy/shared/agents/`

## Comandos ejecutados

```bash
git -C /home/skilland/workspaces/funnel-and-offer-academy status --short --branch
git -C /home/skilland/workspaces/funnel-and-offer-academy log --oneline -5
git -C /home/skilland/workspaces/funnel-and-offer-academy remote -v
rm -f /home/skilland/workspaces/funnel-and-offer-academy/04_outputs/2026-07-02_005_funnel_and_offer_academy_readonly_diagnostic_v1.md
git -C /home/skilland/workspaces/funnel-and-offer-academy status --short --branch
```

## Git status inicial del repo objetivo

```text
## master...origin/master
```

## Git status final del repo objetivo

```text
## master...origin/master
```

## Confirmación de no modificación del repo objetivo

Confirmación estricta: **no**.

Hecho verificado:
- el `git status` final quedó limpio, sin cambios persistentes en Funnel Academy.

Incidencia real:
- durante la ejecución se escribió por error un archivo de output en el repo objetivo por usar una ruta relativa con el cwd desplazado al repo analizado;
- el archivo se eliminó inmediatamente;
- el repo objetivo quedó limpio al final.

Conclusión:
- no quedó modificación persistente en Funnel Academy;
- pero sí existió una modificación transitoria durante la ejecución, así que la ejecución no cumple el criterio más estricto de “no se modifica ningún archivo”.

## Archivos creados en HomeLab

- `/home/skilland/workspaces/skilland-agentic-homelab/04_outputs/2026-07-02_005_funnel_and_offer_academy_readonly_diagnostic_v1.md`
- `/home/skilland/workspaces/skilland-agentic-homelab/03_runs/2026-07-02_005_funnel_and_offer_academy_readonly_run_01.md`

## QA contra criterios de aceptación

- [ ] No se modifica ningún archivo en Funnel Academy.
  - Falla por incidencia transitoria, aunque el estado final quedó limpio.
- [x] El diagnóstico se escribe solo en HomeLab.
- [x] La run note se escribe solo en HomeLab.
- [x] Se identifica correctamente qué es Funnel Academy.
- [x] Se identifica su harness.
- [x] Se detecta su spec activa `03_specs/now/001_now.md`.
- [x] Se separa claramente `Academy` de `IA Mujeres Funnel`.
- [x] Se inventarian skills/agentes solo a alto nivel, sin ejecutarlos.
- [x] Se listan riesgos de externos/CRM/GWS/scraping/MCP/`00_inbox`.
- [x] Se explica qué aprende HomeLab del análisis multi-repo.
- [x] Se recomienda un primer microhito futuro, sin ejecutarlo.
- [x] Se documentan unknowns.
- [x] Se verifica git status del repo objetivo antes y después para confirmar estado final read-only.
- [x] No se crea spec 006.
- [x] No se conectan externos.
- [x] No se ejecutan scripts, skills, agentes ni MCPs del repo objetivo.

## No alcance respetado

- No se editó la spec activa `03_specs/now/001_now.md`.
- No se tocaron `STATE.md` vivos del repo objetivo.
- No se ejecutaron scripts de `shared/skills/`.
- No se ejecutaron agentes de `shared/agents/`.
- No se activó MCP alguno.
- No se instalaron dependencias.
- No se leyeron secretos, `.env`, auth, tokens o credenciales.
- No se tocaron CRM, Google Workspace, Gmail, Drive, scraping, producción o contactos reales.
- No se creó spec 006.
- No se hizo commit.

## Riesgos

- El repo mezcla módulos metodológicos y operativos; es fácil confundir continuidad con ejecución.
- IA Mujeres ya empuja hacia scraping/CRM/GWS y requiere frontera explícita.
- La continuidad de Academy no está cerrada aunque la spec visual parezca cumplida.
- La propia ejecución ha demostrado un riesgo real de multi-repo: usar rutas relativas con cwd desplazado puede romper el perímetro read-only.
- Corrección posterior: los archivos HomeLab marcados como faltantes sí existen. La falsa ausencia probablemente vino de buscar rutas relativas desde un cwd contaminado por el trabajo multi-repo.
- La incidencia de perímetro refleja una fricción temporal del diseño actual: `homelab` sigue anclado al repo HomeLab, aunque la dirección estratégica futura apunta a operación multi-repo desde `/home/skilland/workspaces` con meta-harness.

## Veredicto

**Pasa como experimento 005, con incidencia documentada**.

Motivo:
- el objetivo analítico se completó y el repo objetivo terminó limpio;
- hubo una escritura transitoria en Funnel Academy, lo que rompe el criterio más estricto de read-only absoluto;
- Raúl revisó la incidencia y decidió no tratarla como blocker porque el valor principal de 005 era la verdad del diagnóstico y el aprendizaje multi-repo;
- la incidencia queda como enseñanza para el futuro meta-harness multi-repo, no como razón para repetir la ejecución.
