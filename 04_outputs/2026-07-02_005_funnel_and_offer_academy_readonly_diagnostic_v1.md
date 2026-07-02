# 005 — Diagnóstico read-only de Funnel Academy

## 1. Resumen en cristiano

HomeLab ha comprobado que Hermes puede aterrizar en un repo real ajeno, respetar su harness y producir criterio útil sin tocar nada persistente allí. `funnel-and-offer-academy` no es un repo de app tradicional: es una fábrica docs-first de metodología, conocimiento operativo y outputs comerciales. Tiene dos módulos vivos claramente distintos: `Academy`, orientado a destilación metodológica de funnels/offers, e `ia-mujeres-funnel`, orientado a un sprint comercial ya preparado para handoff hacia scraping/CRM/GWS pero no para ejecución dentro de este repo.

El diagnóstico read-only sugiere que el siguiente microhito seguro no es “seguir trabajando el repo” a ciegas, sino mapear su continuidad operativa: qué está vivo, qué está a medio cerrar, qué depende de humanos y qué exige otro repo o sistemas externos.

## 2. Repo analizado

- Nombre: `funnel-and-offer-academy`
- Path: `/home/skilland/workspaces/funnel-and-offer-academy`
- Remote verificado: `git@github.com:RaulAM7/funnel-and-offer-academy.git`
- Branch verificada: `master...origin/master`
- Últimos commits verificados:
  - `0e344e9 update`
  - `4ba3cda update`
  - `09015c1 Update IA Mujeres email 1 v4.1`
  - `f9b7b60 update`
  - `42ae2da update`

## 3. Alcance read-only aplicado

Hechos verificados:
- Solo se han leído archivos y metadatos git del repo objetivo.
- No se ha ejecutado ningún script, skill, agente ni MCP del repo objetivo.
- No se han leído secretos, `.env`, credenciales ni auth.
- No se ha trabajado `00_inbox/` en profundidad.
- Todos los outputs finales de esta ejecución se han escrito solo en HomeLab.

Incidencia a declarar:
- Durante la ejecución se escribió por error un archivo de diagnóstico en el repo objetivo al usar una ruta relativa con el cwd desplazado al repo analizado.
- Se eliminó inmediatamente y el `git status` final del repo objetivo volvió a limpio.
- No quedó modificación persistente en Funnel Academy, pero la incidencia existió y afecta al veredicto estricto de la spec.

## 4. Qué es Funnel Academy

Hechos verificados:
- Según `README.md`, el repo existe para convertir estudio serio sobre funnels y offers en metodología propia y activos operativos reutilizables.
- Según `02_context/BRIEF.md`, funciona como academia interna + laboratorio de I+D + cantera de skills y agentes.
- Según `README.md`, su principio central es: el usuario estudia y Claude gestiona.
- Según `02_context/FACTS.md`, el repo está pensado para alimentar sistemas downstream como Sales OS y Agentic Business OS.

Inferencia razonable:
- No es solo un repositorio de conocimiento. Es una fábrica de destilación metodológica y de preparación de activos para uso operativo posterior en otros sistemas/repos.

## 5. Qué produce

Hechos verificados desde `README.md` y outputs observados:
- extracciones estructuradas por bloque de estudio;
- síntesis de obra;
- síntesis de dominio;
- catálogo de blueprints;
- método interno emergente;
- assets comerciales y handoffs listos para revisión/ejecución humana en módulos de campaña como `ia-mujeres-funnel`.

## 6. Mapa operativo

### Carpetas principales

- `00_inbox/` — material crudo de entrada. Solo inventariado superficialmente.
- `01_harness/` — reglas, stack, taskflow, índice de skills.
- `02_context/` — memoria destilada del proyecto.
- `03_specs/` — spec activa, backlog y decisiones.
- `04_outputs/` — entregables finales y módulos vivos.
- `05_scratch/` — trabajo intermedio.
- `shared/` — skills y agentes reutilizables.
- `runners/` — notas para operar con agentes externos.

### Archivos clave

- `AGENTS.md`
- `CLAUDE.md`
- `README.md`
- `01_harness/RULES.md`
- `01_harness/STACK.md`
- `01_harness/TASKFLOW.md`
- `02_context/BRIEF.md`
- `02_context/FACTS.md`
- `02_context/CONSTRAINTS.md`
- `03_specs/now/001_now.md`
- `04_outputs/academy/STATE.md`
- `04_outputs/academy/INTERACTION-DESIGN.md`
- `04_outputs/ia-mujeres-funnel/STATE.md`

### Módulos vivos

#### 1) `academy`

Hechos verificados:
- Módulo activo declarado en `README.md`.
- `04_outputs/academy/STATE.md` marca:
  - dominio activo: `funnels`
  - autor activo: `russell-brunson`
  - libro activo: `dotcom-secrets`
  - fase: `block-work`
  - bloque activo: `block-01`
  - capa visual: habilitada
- El estado dice que solo `Secret-01` está trabajado en detalle y que el siguiente paso recomendado es continuar con `Secret-02`.
- La spec activa del repo (`03_specs/now/001_now.md`) corresponde a la integración de la capa visual Academy y sus criterios aparecen marcados como cumplidos.

#### 2) `ia-mujeres-funnel`

Hechos verificados:
- `04_outputs/ia-mujeres-funnel/STATE.md` lo declara como proyecto `ia-mujeres-funnel` con estado `icp2_ready_for_scraping_handoff`.
- El objetivo del módulo conecta estrategia, ICP, CRM Twenty, Google Workspace CLI, secuencia de emails y seguimiento.
- El estado dice explícitamente que Funnel Academy no scrapea, no toca CRM, no toca GWS, no crea workflows, no crea CSVs reales y no modifica contactos reales.
- El siguiente paso actual está fuera de este repo: handoff al repo de scraping para producir `Canarias V1`.

### Harness

Hechos verificados:
- El repo tiene harness propio con `AGENTS.md`, `CLAUDE.md`, `01_harness/`, `02_context/`, `03_specs/`, `04_outputs/`, `05_scratch/`, `shared/`.
- `RULES.md` refuerza docs-first, una spec activa a la vez, outputs en `04_outputs/` y QA explícito.
- `STACK.md` confirma workspace docs-first con tooling ligero y capa visual alrededor de Excalidraw/MCP.
- `TASKFLOW.md` conserva el flujo Seed → Distill → Spec → Ship → QA.

### Skills y agentes a alto nivel

Hechos verificados:
- Skills inventariadas a alto nivel: `visualize-study-block`, `write-spec`, `synthesize-domain`, `synthesize-book`, `skill-creator`, `build-study-itinerary`, `catalog-blueprints`, `icp-definer`, `distill-study-block`, `qa-review`, `ship-output`, `distill-context`, `initial-context-building`, `manage-academy-cycle`.
- Agentes inventariados a alto nivel: `visual-editor`, `distiller`, `reviewer`, `study-distiller`, `method-synthesizer`, `academy-orchestrator`, `prospector`, `maker`, `planner`, `blueprint-cataloger`.

Observación importante:
- No se han ejecutado ni inspeccionado internamente esos skills/agentes más allá del inventario de archivos, porque esta spec lo prohíbe.

## 7. Estado actual

### Spec activa

Hechos verificados:
- La spec activa detectada es `03_specs/now/001_now.md`.
- Su outcome es integrar la capa visual de Academy.
- Sus acceptance criteria están marcados como cumplidos dentro del propio documento.

### Estado Academy

Hechos verificados:
- `STATE.md` refleja trabajo parcial real, no cierre limpio:
  - frontmatter dice `blocks_completed: 0`
  - la tabla dice `1/5 secrets` dentro del bloque 01
  - el tracker del libro dice `1/5`
- Hay, por tanto, una tensión entre “spec visual completada” y “módulo Academy todavía en progreso”.

Inferencia:
- El repo parece tener la capa visual integrada, pero la continuidad operativa del módulo no está cerrada ni convertida aún en una decisión clara de “seguir / cerrar / pausar / archivar”.

### Estado IA Mujeres Funnel

Hechos verificados:
- El sprint estratégico/copy se presenta como listo para cierre dentro de Funnel Academy.
- El siguiente paso operativo ya no pertenece aquí, sino a scraping/CRM/GWS.
- Existen handoffs preparados para ejecución humana y/o en otros repos.

Inferencia:
- Este módulo parece más cerca de una frontera inter-repo y de sistemas externos que de trabajo interno adicional en Funnel Academy.

### Backlog y decisiones relevantes

Hechos verificados:
- El backlog mantiene mucho trabajo metodológico pendiente sobre Brunson/Hormozi y extensión de la capa visual.
- En decisiones aparece la adopción de Excalidraw MCP como runtime visual primario con fallback local.
- Las decisiones y el backlog refuerzan que este repo sigue vivo, pero con frentes distintos: academia metodológica y funnel aplicado.

## 8. Riesgos y no alcance

### Externos

- `ia-mujeres-funnel` ya apunta a otro repo de scraping y a sistemas CRM/GWS.
- Meterse ahí sin spec propia rompe el perímetro seguro de HomeLab.

### CRM / GWS / scraping

Hechos verificados:
- El propio `STATE.md` de IA Mujeres menciona CRM Twenty, Google Workspace CLI y handoff al repo de scraping.
- También dice explícitamente que este repo no debe ejecutar esas partes.

### MCP visual

Hechos verificados:
- El repo tiene `.mcp.json` y una spec activa sobre Excalidraw MCP.
- Tocar o ejecutar esa capa habría sido salirse del alcance 005.

### `00_inbox`

Hechos verificados:
- Solo se inventarió superficialmente por nombres de archivo.
- Contiene material fuente de Hormozi, Brunson, Valdo y README del inbox.

Riesgo:
- Leerlo a fondo habría convertido 005 en resumen de fuentes y no en diagnóstico operativo del repo.

### Outputs vivos

- `04_outputs/academy/STATE.md` y `04_outputs/ia-mujeres-funnel/STATE.md` son outputs vivos de continuidad.
- Manipularlos sin spec propia habría sido operar el repo, no diagnosticarlo.

### Secretos

- No se revisaron `.env`, auth, tokens, credenciales ni configuraciones sensibles.
- Sigue siendo `Unknown` si existen o no más secretos fuera de los paths leídos, porque esa búsqueda no formaba parte del alcance seguro.

## 9. Oportunidades detectadas

1. **Mapa de continuidad multi-módulo**
   - Separar claramente qué está vivo, qué está terminado, qué está bloqueado y qué depende de repos/sistemas externos.

2. **Cierre formal de la spec visual vs continuidad Academy**
   - La spec 001 parece cumplida en integración visual, pero el módulo Academy sigue operativo y parcialmente avanzado. Conviene distinguir “spec cerrable” de “módulo terminado”.

3. **Frontera inter-repo más explícita**
   - IA Mujeres ya roza scraping/CRM/GWS. Merece una interfaz de handoff más explícita para que futuros agentes no crucen el perímetro sin control humano.

4. **Taxonomía de estados de módulo**
   - Este repo ya no es lineal. Le vendría bien un vocabulario consistente: activo, en progreso, listo para handoff, pendiente de cierre humano, congelado, etc.

## 10. Qué aprende HomeLab de este tipo de repo

Hechos verificados + aprendizaje operativo:
- Hermes sí puede operar como lector disciplinado de un repo real con vida propia.
- Un repo de negocio no siempre es “código” ni “documentación”: puede ser fábrica híbrida de método, estado, assets y handoffs.
- Multi-repo no debe empezar por automatizar; debe empezar por aprender perímetros, estados y fronteras de responsabilidad.
- El valor de HomeLab aquí no es tocar Funnel Academy, sino demostrar criterio para no tocarlo cuando no toca.
- La incidencia de escritura transitoria no invalida el diagnóstico: muestra una fricción de la arquitectura temporal actual, donde `homelab` sigue anclado al repo HomeLab mientras intenta observar otros repos por path absoluto.
- Aprendizaje estratégico: si HomeLab aspira a funcionar como sistema operativo agentic multi-repo, más adelante necesitará un cwd/base superior —probablemente `/home/skilland/workspaces`— y un meta-harness capaz de coordinar harnesses internos por repo.
- Hasta que exista ese meta-harness, los diagnósticos multi-repo deben extremar paths absolutos; pero esa fricción no debe confundirse con el objetivo final.

## 11. Primer microhito recomendado, sin ejecutarlo

### Recomendación principal

`funnel_academy_repo_continuity_map`

Por qué:
- es el paso más seguro;
- produce claridad real;
- no exige tocar externos;
- puede vivir todavía como análisis read-only o con escritura controlada y explícita posterior;
- ayuda a decidir si luego conviene cerrar formalmente la spec activa, retomar Academy o mover IA Mujeres a otro repo.

### Qué debería hacer ese microhito

- mapear módulos vivos del repo;
- distinguir estado del módulo vs estado de la spec;
- marcar dependencias externas y próximos repos/sistemas;
- proponer una decisión humana por módulo: continuar, cerrar, congelar o handoff.

## 12. Unknowns

- Corrección posterior: los archivos HomeLab que la ejecución marcó como faltantes sí existen. La falsa ausencia probablemente vino de buscar rutas relativas desde un cwd contaminado por el trabajo multi-repo. No se considera unknown de fondo del proyecto.
- `Unknown`: no está formalmente decidido en el repo si `03_specs/now/001_now.md` debe cerrarse ya o seguir abierta como paraguas de continuidad.
- `Unknown`: no está explicitado si `ia-mujeres-funnel` debe cerrarse en este repo o solo mantenerse como repositorio de handoff histórico.
- `Unknown`: no está documentado aquí el estado real de los repos/sistemas downstream que deberían recibir el handoff.
- `Unknown`: no se verificó el contenido interno de `.mcp.json`, solo su existencia por inventario de archivos, porque ejecutar o profundizar la capa MCP no era necesario para 005.

## 13. Veredicto de revisión humana

Pasa como experimento 005.

Motivo:
- el diagnóstico es útil y estratégicamente correcto;
- el repo objetivo terminó limpio;
- la incidencia de perímetro quedó declarada y se convirtió en aprendizaje sobre la arquitectura temporal actual;
- Raúl prioriza la verdad del diagnóstico y el aprendizaje multi-repo sobre el cumplimiento perfecto de un perímetro read-only que existe por una configuración provisional de `homelab`.

La ejecución no debe repetirse solo por la escritura transitoria. La lección queda recogida para el futuro diseño de operación multi-repo/meta-harness.

## 14. Siguiente paso recomendado

No crear 006 automáticamente.

Siguiente paso recomendado para revisión humana:
- revisar este diagnóstico;
- decidir si el siguiente microhito será un `continuity map` del repo;
- y solo después decidir si procede cerrar formalmente la spec visual, retomar Academy o mover el foco al handoff de IA Mujeres.
