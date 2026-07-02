# 005 Hermes First Real Repo Read-Only Operator

Fecha: 2026-07-02

## Resultado esperado

Hermes `homelab`, operando desde el repo HomeLab, analiza en modo read-only el repo real:

```text
/home/skilland/workspaces/funnel-and-offer-academy
```

y deja en HomeLab un diagnóstico operativo útil para decidir el siguiente microhito.

El resultado no es modificar Funnel Academy. El resultado es comprobar si Hermes puede aterrizar en un repo real con vida propia, respetar su harness, entender su estado y producir criterio accionable sin tocar nada.

## Resumen en cristiano

Este microhito es el primer paso fuera de “Hermes sobre Hermes”.

Hasta ahora HomeLab ha servido para instalar, entender y dar identidad/memoria a Hermes. Ahora toca probar una capacidad más real: usar Hermes como lector operativo de otro repo de Skilland/Reboot.

`funnel-and-offer-academy` es buen primer candidato porque no es solo código. Es una fábrica de metodología, producto, conocimiento y activos comerciales: funnels, offers, skills, agentes, blueprints, handoffs y outputs de campañas. Si Hermes puede entender este repo sin tocarlo, HomeLab aprende algo importante sobre operación multi-repo y repos como departamentos/fábricas.

Esta spec no arregla Funnel Academy. No continúa su trabajo. No cierra su spec activa. No ejecuta scripts. No toca CRM, Google Workspace, scraping, MCPs ni externos.

Solo diagnostica en read-only y devuelve criterio.

## Contexto estratégico

- North Star busca una empresa pequeña operable desde la palma de la mano mediante agentes residentes sobre repos, CRM, Drive, Gmail, GitHub, datos, campañas y entregables reales.
- HomeLab es el laboratorio operativo en el VPS real donde esa visión se convierte en capacidades explorables.
- Hermes debe aprender a operar con repos reales como fábricas/departamentos de trabajo, no como carpetas sueltas.
- Codex/Hermes deben distinguir leer, diagnosticar, decidir, implementar y verificar.
- Esta prueba es multi-repo controlada: HomeLab manda y Funnel Academy es objeto read-only.
- Todo aprendizaje, output y trazabilidad de este microhito vive en HomeLab.

## Repo objetivo

```text
Nombre: funnel-and-offer-academy
Path: /home/skilland/workspaces/funnel-and-offer-academy
Remote: git@github.com:RaulAM7/funnel-and-offer-academy.git
Branch observado al crear esta spec: master...origin/master
Últimos commits observados:
- 0e344e9 update
- 4ba3cda update
- 09015c1 Update IA Mujeres email 1 v4.1
- f9b7b60 update
- 42ae2da update
```

Advertencia fuerte: este repo no debe modificarse durante 005.

## Hipótesis inicial sobre Funnel Academy

Desde la lectura mínima previa:

- El repo se define como `Funnel & Offer Design Academy`.
- Su función es convertir estudio serio de funnels/offers en metodología propia y activos operativos reutilizables.
- Tiene harness propio: `AGENTS.md`, `01_harness/`, `02_context/`, `03_specs/`, `04_outputs/`, `05_scratch/`, `shared/`.
- Tiene una spec activa: `03_specs/now/001_now.md`, relacionada con integración de capa visual Academy.
- Tiene un módulo `Academy` con estado vivo en `04_outputs/academy/STATE.md`.
- Tiene un módulo/sprint `ia-mujeres-funnel` con estado en `04_outputs/ia-mujeres-funnel/STATE.md`.
- Contiene skills y agentes propios bajo `shared/skills/` y `shared/agents/`.

La ejecución de esta spec debe verificar, matizar o corregir estas hipótesis con lectura read-only.

## Lecturas obligatorias en HomeLab

Antes de analizar el repo objetivo, leer en HomeLab:

1. `AGENTS.md`
2. `01_harness/RULES.md`
3. `01_harness/STACK.md`
4. `01_harness/TASKFLOW.md`
5. `03_specs/now/005_hermes_first_real_repo_readonly_operator.md`
6. `03_specs/decisions.md`
7. `04_outputs/2026-07-02_hermes_identity_memory_foundation_close_v1.md`
8. `03_runs/2026-07-02_hermes_identity_memory_foundation_close_run_01.md`
9. `02_context/HERMES_PROFILE_FOUNDATION.md`
10. `02_context/HERMES_RUNTIME_NOTES.md`

## Lecturas obligatorias en Funnel Academy

Leer por path absoluto, sin modificar:

1. `/home/skilland/workspaces/funnel-and-offer-academy/AGENTS.md`
2. `/home/skilland/workspaces/funnel-and-offer-academy/README.md`
3. `/home/skilland/workspaces/funnel-and-offer-academy/CLAUDE.md`
4. `/home/skilland/workspaces/funnel-and-offer-academy/01_harness/RULES.md`
5. `/home/skilland/workspaces/funnel-and-offer-academy/01_harness/STACK.md`
6. `/home/skilland/workspaces/funnel-and-offer-academy/01_harness/TASKFLOW.md`
7. `/home/skilland/workspaces/funnel-and-offer-academy/02_context/BRIEF.md`
8. `/home/skilland/workspaces/funnel-and-offer-academy/02_context/FACTS.md`
9. `/home/skilland/workspaces/funnel-and-offer-academy/02_context/CONSTRAINTS.md`
10. `/home/skilland/workspaces/funnel-and-offer-academy/02_context/GLOSSARY.md`
11. `/home/skilland/workspaces/funnel-and-offer-academy/02_context/LINKS.md`
12. `/home/skilland/workspaces/funnel-and-offer-academy/03_specs/now/001_now.md`
13. `/home/skilland/workspaces/funnel-and-offer-academy/03_specs/backlog.md`
14. `/home/skilland/workspaces/funnel-and-offer-academy/03_specs/decisions.md`
15. `/home/skilland/workspaces/funnel-and-offer-academy/04_outputs/academy/STATE.md`
16. `/home/skilland/workspaces/funnel-and-offer-academy/04_outputs/academy/INTERACTION-DESIGN.md`
17. `/home/skilland/workspaces/funnel-and-offer-academy/04_outputs/ia-mujeres-funnel/STATE.md`

También inventariar a alto nivel, sin ejecutar:

- `/home/skilland/workspaces/funnel-and-offer-academy/shared/skills/`
- `/home/skilland/workspaces/funnel-and-offer-academy/shared/agents/`

Sobre `00_inbox/`:

- No leerlo en profundidad.
- No copiar contenido.
- No resumir libros/fuentes.
- Solo inventariar superficialmente si hace falta para entender tipos de insumo.

## Comandos read-only permitidos

En el repo objetivo:

```bash
git -C /home/skilland/workspaces/funnel-and-offer-academy status --short --branch
git -C /home/skilland/workspaces/funnel-and-offer-academy log --oneline -5
git -C /home/skilland/workspaces/funnel-and-offer-academy remote -v
```

También se permite listar archivos/carpetas relevantes usando herramientas de lectura/búsqueda, siempre sin modificar.

## Alcance permitido

- Leer archivos versionados del repo objetivo.
- Inspeccionar estructura del repo objetivo.
- Revisar git status/log/remote del repo objetivo.
- Mapear harness, contexto, specs, outputs, skills y agentes.
- Identificar módulos vivos, estados, riesgos y oportunidades.
- Escribir outputs solo en HomeLab.
- Usar `05_scratch/` de HomeLab para notas temporales si hace falta.
- Separar hechos verificados, inferencias e unknowns.

## Fuera de alcance

Prohibido durante 005:

- modificar cualquier archivo de Funnel Academy;
- editar su spec activa `03_specs/now/001_now.md`;
- cerrar, mover o archivar specs en Funnel Academy;
- continuar Academy block-01 o Secret-02;
- tocar `04_outputs/academy/STATE.md`;
- tocar `04_outputs/ia-mujeres-funnel/STATE.md`;
- ejecutar scripts de `shared/skills/`;
- ejecutar agentes de `shared/agents/`;
- activar MCP Excalidraw o cualquier MCP;
- instalar dependencias;
- leer secretos, `.env`, auth, tokens o credenciales;
- tocar CRM, Google Workspace, Gmail, Drive, scraping, producción o contactos reales;
- crear commits;
- crear issues o PRs;
- crear spec 006;
- conectar externos;
- enviar mensajes reales;
- convertir el diagnóstico en auditoría enterprise extensa.

## Entregables

La ejecución de 005 debe crear en HomeLab:

```text
04_outputs/2026-07-02_005_funnel_and_offer_academy_readonly_diagnostic_v1.md
03_runs/2026-07-02_005_funnel_and_offer_academy_readonly_run_01.md
```

Si se ejecuta en otra fecha, adaptar el prefijo de fecha y documentarlo.

## Estructura mínima del output

`04_outputs/2026-07-02_005_funnel_and_offer_academy_readonly_diagnostic_v1.md` debe incluir:

1. Resumen en cristiano.
2. Repo analizado.
3. Alcance read-only aplicado.
4. Qué es Funnel Academy.
5. Qué produce.
6. Mapa operativo:
   - carpetas principales;
   - archivos clave;
   - módulos vivos;
   - harness;
   - skills/agentes a alto nivel.
7. Estado actual:
   - spec activa;
   - estado Academy;
   - estado IA Mujeres Funnel;
   - backlog/decisiones si son relevantes.
8. Riesgos/no alcance:
   - externos;
   - CRM/GWS/scraping;
   - MCP visual;
   - `00_inbox`;
   - outputs vivos;
   - secretos.
9. Oportunidades detectadas.
10. Qué aprende HomeLab de este tipo de repo.
11. Primer microhito recomendado, sin ejecutarlo.
12. Unknowns.
13. Siguiente paso recomendado.

## Estructura mínima de la run note

`03_runs/2026-07-02_005_funnel_and_offer_academy_readonly_run_01.md` debe incluir:

- objetivo;
- fecha;
- archivos leídos;
- comandos ejecutados;
- git status inicial y final del repo objetivo;
- confirmación de no modificación del repo objetivo;
- archivos creados en HomeLab;
- QA contra criterios de aceptación;
- no alcance;
- riesgos;
- veredicto: pasa / no pasa.

## Criterios de aceptación

- [ ] No se modifica ningún archivo en Funnel Academy.
- [ ] El diagnóstico se escribe solo en HomeLab.
- [ ] La run note se escribe solo en HomeLab.
- [ ] Se identifica correctamente qué es Funnel Academy.
- [ ] Se identifica su harness.
- [ ] Se detecta su spec activa `03_specs/now/001_now.md`.
- [ ] Se separa claramente `Academy` de `IA Mujeres Funnel`.
- [ ] Se inventarian skills/agentes solo a alto nivel, sin ejecutarlos.
- [ ] Se listan riesgos de externos/CRM/GWS/scraping/MCP/`00_inbox`.
- [ ] Se explica qué aprende HomeLab del análisis multi-repo.
- [ ] Se recomienda un primer microhito futuro, sin ejecutarlo.
- [ ] Se documentan unknowns.
- [ ] Se verifica git status del repo objetivo antes y después para confirmar read-only.
- [ ] No se crea spec 006.
- [ ] No se conectan externos.
- [ ] No se ejecutan scripts, skills, agentes ni MCPs del repo objetivo.

## Riesgos

- Hermes puede intentar operar Funnel Academy en vez de diagnosticarlo.
- Puede confundir outputs vivos con tareas a ejecutar.
- Puede tocar CRM/GWS/scraping por seguir handoffs operativos.
- Puede leer demasiado `00_inbox` y convertir el diagnóstico en resumen de fuentes.
- Puede ignorar el harness del repo objetivo.
- Puede escribir outputs en el repo equivocado.
- Puede hacer una auditoría demasiado grande y poco accionable.
- Puede recomendar continuar Academy cuando antes conviene mapear continuidad o cerrar la spec activa.

## Recomendación de estilo

- Español.
- Directo.
- Estratégico pero accionable.
- No enterprise.
- No paja académica.
- Separar hechos verificados, inferencias e unknowns.
- Priorizar utilidad para decidir el siguiente microhito.

## Orientación para el primer microhito recomendado

La ejecución debe recomendar un primer microhito futuro. No debe ejecutarlo.

Candidatos esperables, a validar por diagnóstico:

1. `funnel_academy_repo_continuity_map`
   - Mapa de continuidad del repo: módulos vivos, terminado, bloqueado, siguiente decisión humana.
   - Muy seguro, puede producir valor sin tocar el repo objetivo.

2. `funnel_academy_close_active_visual_spec`
   - Verificar si `03_specs/now/001_now.md` está realmente completada y cerrarla formalmente dentro de Funnel Academy.
   - Más accionable, pero ya implica escritura en el repo objetivo, por tanto sería posterior a 005 y con spec propia.

3. `funnel_academy_resume_academy_block_01`
   - Retomar Academy desde `STATE.md` y continuar Secret-02.
   - Potencialmente valioso, pero más profundo y dependiente de contenido de `00_inbox`.

4. `ia_mujeres_funnel_handoff_review`
   - Revisar handoff IA Mujeres hacia scraping/CRM/GWS.
   - Estratégico, pero más cercano a sistemas externos; no debería ser el primer paso salvo decisión explícita.

## QA final de la ejecución

Antes de cerrar la ejecución de 005, verificar:

```bash
git -C /home/skilland/workspaces/funnel-and-offer-academy status --short --branch
find 03_specs/now -maxdepth 1 -type f -print | sort
test -f 04_outputs/2026-07-02_005_funnel_and_offer_academy_readonly_diagnostic_v1.md
test -f 03_runs/2026-07-02_005_funnel_and_offer_academy_readonly_run_01.md
git status --short --branch
```

La spec 005 debe seguir activa hasta revisión humana posterior. No archivarla automáticamente.

## Siguiente paso tras ejecutar 005

Raúl y la sesión arquitecta revisarán el diagnóstico y decidirán si el siguiente microhito será:

- un mapa de continuidad;
- cierre formal de la spec activa de Funnel Academy;
- retomar Academy;
- revisar IA Mujeres handoff;
- u otro paso derivado del diagnóstico.

No decidir 006 automáticamente.
