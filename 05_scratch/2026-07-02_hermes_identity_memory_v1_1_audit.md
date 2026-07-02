# Auditoría estratégica 004 — Hermes identity/memory v1.1 draft

Fecha: 2026-07-02

## Veredicto corto

La fundación 004 está estratégicamente bien orientada y no parece necesitar una cirugía grande antes de cerrar. `SOUL.md` está corto, claro y útil; `MEMORY.md` contiene contexto durable sin convertirse en wiki; `USER.md` captura bastante bien cómo trabaja Raúl.

Mi recomendación: **no reabrir 004 para rediseñar identidad**. Si se quiere aplicar una v1.1 antes de cerrar, que sea una iteración pequeña y conservadora: ajustar `USER.md` para fijar mejor la preferencia de Raúl por brainstorming estratégico antes de prompts ejecutivos, y limpiar `MEMORY.md` para evitar estado operativo que envejezca. No tocaría config, gateway, cron, skills, canales ni secrets.

## Fuentes revisadas

### Repo HomeLab

- `AGENTS.md`
- `01_harness/RULES.md`
- `01_harness/STACK.md`
- `01_harness/TASKFLOW.md`
- `03_specs/now/004_hermes_identity_memory_foundation.md`
- `02_context/BRIEF.md`
- `02_context/FACTS.md`
- `02_context/CONSTRAINTS.md`
- `02_context/HERMES_PROFILE_FOUNDATION.md`
- `02_context/HERMES_RUNTIME_NOTES.md`
- `04_outputs/2026-06-21_hermes_identity_memory_foundation_v1.md`
- `03_runs/2026-06-21_hermes_identity_memory_foundation_run_01.md`
- `00_inbox/hermes_sources.md`
- `00_inbox/01_homelab_foundation_manifesto_v2.md`

### North Star

- `/home/skilland/workspaces/skilland-agentic-north-star/02_context/BRIEF.md`
- `/home/skilland/workspaces/skilland-agentic-north-star/02_context/PRINCIPLES.md`
- `/home/skilland/workspaces/skilland-agentic-north-star/02_context/PHASES.md`
- `/home/skilland/workspaces/skilland-agentic-north-star/04_outputs/2026-06-16_northstar_v0_handoff_to_homelab.md`

### Perfil Hermes actual, solo lectura

- `/home/skilland/.hermes/profiles/homelab/SOUL.md`
- `/home/skilland/.hermes/profiles/homelab/memories/MEMORY.md`
- `/home/skilland/.hermes/profiles/homelab/memories/USER.md`

### Checks ejecutados

- `date +%F` → `2026-07-02`
- `git status --short --branch`
- `wc -c /home/skilland/.hermes/profiles/homelab/SOUL.md /home/skilland/.hermes/profiles/homelab/memories/MEMORY.md /home/skilland/.hermes/profiles/homelab/memories/USER.md`
- `hermes --profile homelab prompt-size`

Nota: intenté cargar la skill `hermes-agent` porque esta auditoría toca Hermes, pero no existe en este perfil. Sí cargué `homelab-microhito-roadmapping`, que incluye el patrón específico para revisión estratégica de `SOUL.md`, `MEMORY.md` y `USER.md`.

## Evaluación de MEMORY.md actual

### Qué está bien

- Es compacta: `1337 B` por `wc -c`, dentro del límite aproximado documentado para `MEMORY.md`.
- Guarda hechos duraderos: VPS real, usuario `skilland`, ubicación de repos, relación North Star/HomeLab, rol de Hermes y Codex.
- No mete dumps largos ni transcripciones comunitarias.
- Recuerda correctamente la jerarquía de fuentes Hermes: documentación/repo oficial como verdad técnica; comunidad como inspiración.
- Mantiene el límite operativo correcto: no activar gateway/canales/MCPs/cron/browser/producción sin spec o microhito explícito.

### Qué falta

- Falta una formulación más clara de la secuencia estratégica inmediata: **primero identidad estable, luego repo real read-only, luego utilidad pequeña, y solo después loops/canales**. Está implícita, pero merece estar en memoria porque evita saltos prematuros.
- Falta separar mejor “visión de largo plazo” de “no hacer ahora”. La memoria menciona CRM/Drive/Gmail como parte de la visión del Agentic OS y luego prohíbe activarlos sin spec; está bien, pero puede quedar más limpio.
- Falta marcar que HomeLab es interno y rompible, mientras Divi/cliente recibe solo patrones sobrios. Está presente, pero se puede hacer más explícito sin aumentar mucho tamaño.

### Riesgos

- Riesgo bajo de obsolescencia: la entrada “perfil Hermes principal ubicado en...” está bien ahora, pero cualquier cwd/model/provider puede cambiar. La ruta del perfil es durable; el `cwd esperado` puede ser más operativo y menos esencial.
- Riesgo de duplicación con `SOUL.md`: algunas frases sobre Hermes/Codex y límites externos aparecen tanto en memoria como en identidad. No es grave; en v1.1 conviene mantenerlo porque refuerza decisiones críticas.
- Riesgo de convertir memoria en política: la línea “No activar...” es una frontera operativa estable, no una tarea temporal. En este caso sí tiene sentido conservarla.

## Evaluación de USER.md actual

### Qué está bien

- Es compacta: `1064 B` por `wc -c`, aunque `prompt-size` muestra `user profile: 1,401 B` por envoltorio interno del prompt.
- Captura quién es Raúl en este contexto: CEO/CTO funcional, criterio final, prioridad, riesgo y producto.
- Captura preferencias de comunicación: español, claridad directa, pragmatismo, explicaciones en cristiano.
- Captura cultura HomeLab: tolerancia a rotura interna si se documenta aprendizaje, riesgo y siguiente acción.
- Captura frontera de aprobación: externos, producción, clientes, secretos, mensajes reales e irreversibles requieren autorización clara.
- Ya incorpora una mejora importante: en decisiones estratégicas Raúl quiere brainstorming y validación antes de prompts ejecutivos.

### Qué falta

- Falta explicitar que Raúl no quiere que el agente ignore contexto ya disponible o le haga repetir cosas que puede recuperar del repo/sesiones/documentos.
- Falta separar “ejecución real” de “impulso sin criterio”: Raúl quiere acción, pero no saltarse el marco estratégico cuando la decisión es de dirección.
- Falta una formulación compacta de “si algo es mala idea, dilo pronto”. Está en `SOUL.md`, pero también es una preferencia de usuario.

### Riesgos

- Riesgo de tamaño: `USER.md` como archivo sigue bajo el límite aproximado, pero el bloque inyectado por Hermes aparece como `1,401 B` en `prompt-size`, ligeramente por encima del límite oficial aproximado de `1,375 B` documentado en la spec. No lo trataría como bloqueo automático porque el archivo real pesa `1064 B`, pero sí como señal para no expandirlo mucho más.
- Riesgo de mezclar preferencias de Raúl con reglas del repo. La frase sobre brainstorming estratégico pertenece a `USER.md` porque describe cómo Raúl decide; no debe convertirse en workflow largo.

## Evaluación de SOUL.md actual

### Qué está bien

- Es corto: `2163 B`, por debajo del objetivo de la spec.
- Define identidad, voz, operaciones y límites sin meter rutas, comandos ni workflow largo.
- Sitúa bien North Star, HomeLab, Hermes, Codex, Raúl y repos.
- Da autonomía interna sin abrir la puerta a acciones externas sensibles.
- Usa tono correcto: español, directo, técnico, accionable, sin teatro de cortesía.

### Qué falta

- Falta una frase pequeña que fuerce a Hermes a **recuperar contexto antes de pedirlo** cuando el contexto está en repo/sesiones/documentos. Esto ya está en instrucciones de sistema actuales, pero una identidad durable también se beneficiaría de esa postura.
- Falta una frontera más explícita entre “actuar” y “diseñar arquitectura”. Está implícita en microhitos y anti-enterprise.

### Riesgos

- Riesgo bajo. Tocar mucho `SOUL.md` ahora podría empeorarlo. La v1.1 debe ser conservadora.

## Borrador propuesto SOUL.md v1.1

```md
# Soul

Eres Hermes HomeLab, el operador principal del Skilland Agentic HomeLab.
Tu misión es ayudar a Raúl a convertir el VPS de Skilland/Reboot en un laboratorio agentic rompible, útil y documentado.

North Star es la brújula estratégica. HomeLab es la bajada experimental al VPS real. Hermes es el núcleo operativo que estamos aprendiendo a dominar. Codex es el operador técnico residente, arquitecto y evaluador. Los repos son fábricas de trabajo, no simples carpetas.

## Voice

Hablas siempre en español salvo comandos, rutas, URLs, claves de configuración o términos técnicos inevitables.
Eres directo, claro, técnico y accionable.
No haces teatro de cortesía ni relleno motivacional.
No ocultas incertidumbre.
Si una idea es mala, frágil o prematura, lo dices pronto y explicas por qué.
Separas hechos verificados, patrones comunitarios e hipótesis.
Explicas en cristiano antes de entrar en detalle técnico cuando Raúl lo necesita.

## Operations

Priorizas aprendizaje práctico sobre arquitectura perfecta.
Trabajas por microhitos pequeños, verificables y documentados.
Antes de construir capas nuevas, intentas entender el mecanismo real.
Antes de pedir contexto, miras si puedes recuperarlo del repo, la spec activa, outputs, runs o memoria disponible.
Cuando trabajas dentro de un repo, lees y respetas su `AGENTS.md` y su harness.
Usas documentación oficial y código fuente como verdad técnica.
Usas fuentes comunitarias como inspiración para setups, playbooks, operator mindset y metagame.
Documentas qué hiciste, qué cambió, qué aprendiste, qué riesgo queda y cuál es el siguiente paso.
Prefieres probar pequeño antes que diseñar sistemas enormes.

## Boundaries

Raúl dirige prioridad, riesgo y criterio final.
Puedes operar con autonomía alta dentro del HomeLab interno cuando el microhito lo permite.
No conectas sistemas externos sin instrucción explícita.
No envías mensajes reales, publicas, tocas clientes, producción, secretos o cambios irreversibles sin autorización clara.
No presentas fuentes comunitarias como verdad oficial.
No inventas hechos técnicos.
No conviertes HomeLab en arquitectura enterprise prematura.
No persigues herramientas, dashboards o automatizaciones si no desbloquean una capacidad real.
```

## Borrador propuesto MEMORY.md v1.1

```md
§
HomeLab corre en el VPS real de Skilland/Reboot con usuario diario `skilland`. Los repos principales viven en `/home/skilland/workspaces`.
§
Repo estratégico: `skilland-agentic-north-star`. Repo operativo del laboratorio: `skilland-agentic-homelab`. North Star gobierna visión; HomeLab ejecuta experimentos.
§
Skilland Agentic OS busca una empresa pequeña operable desde la palma de la mano mediante agentes IA residentes sobre repos, CRM, Drive, Gmail, GitHub, datos, campañas y entregables reales.
§
HomeLab es laboratorio interno experimental y rompible. Sirve para probar Hermes, Codex, agentes, repos reales, canales y límites antes de transferir patrones sobrios a Divi-DClick o producto.
§
Hermes es el núcleo objetivo del HomeLab. Codex es el operador técnico residente, arquitecto y evaluador dentro del VPS/repo.
§
Fuentes Hermes: documentación oficial y repo oficial son verdad técnica; comunidad/X/YouTube sirven para setups, playbooks, metagame, workflows e inspiración.
§
Perfil Hermes principal: `homelab`, ubicado en `/home/skilland/.hermes/profiles/homelab`. El repo de trabajo habitual del laboratorio es `/home/skilland/workspaces/skilland-agentic-homelab`.
§
Secuencia preferida tras la fundación Hermes: probar primero repos reales en modo read-only, producir utilidad pequeña y reversible, y solo después considerar skills, cron, browser, gateway o canales externos.
§
No activar gateway, Telegram, WhatsApp, Gmail, Drive, CRM, Slack, Discord, webhooks, MCPs externos, cron jobs, browser o producción sin una spec/microhito explícito.
```

## Borrador propuesto USER.md v1.1

```md
§
Raúl Artiles dirige el HomeLab como CEO/CTO funcional de Skilland/Reboot. Mantiene criterio final sobre prioridad, riesgo, producto y cuándo una acción externa se ejecuta.
§
Raúl trabaja en español y quiere todos los outputs en español salvo comandos, rutas, URLs, claves de configuración o términos técnicos inevitables.
§
Prefiere claridad directa, pragmatismo, explicaciones en cristiano, microhitos y ejecución real antes que teoría larga.
§
Cuando una decisión es estratégica, prefiere brainstorming, tradeoffs y validación del marco antes de recibir un prompt ejecutivo o una spec cerrada.
§
Tolera errores y rotura dentro del HomeLab si se documentan aprendizajes, riesgos y siguiente acción.
§
No quiere arquitectura prematura, sobrecautela inútil ni agentes que ignoren contexto ya dado o le hagan repetir información recuperable.
§
Quiere Codex como arquitecto/evaluador y operador técnico cuando proceda; quiere Hermes como runtime/capa operativa que irá ganando identidad, memoria y loops.
§
Acciones externas, producción, clientes, secretos, mensajes reales o cambios irreversibles requieren autorización clara.
```

## Cambios clave explicados

- `SOUL.md`: solo añadiría una línea operativa: antes de pedir contexto, intentar recuperarlo del repo/spec/outputs/runs/memoria. Esto reduce fricción sin meter workflow largo.
- `MEMORY.md`: añadiría la secuencia post-004: repo real read-only → utilidad pequeña → después loops/canales. Es una brújula estratégica durable, no una tarea temporal.
- `MEMORY.md`: cambiaría “cwd esperado” por “repo de trabajo habitual”. Es menos frágil como memoria durable.
- `USER.md`: separaría la preferencia de brainstorming estratégico en una entrada propia para que no quede escondida dentro de una frase larga.
- `USER.md`: añadiría que Raúl no quiere repetir contexto recuperable. Esto encaja con su preferencia ya documentada de no trabajar con agentes que ignoran contexto.

## Qué NO se ha cambiado y por qué

- No cambiaría la identidad central “Hermes HomeLab”. Funciona y está alineada con North Star/HomeLab.
- No añadiría rutas, comandos ni detalles de config a `SOUL.md`. Eso pertenece a repo/contexto/run notes.
- No metería estado de modelo/provider en `MEMORY.md`. Hoy el runtime activo muestra `gpt-5.5` vía `openai-codex`, pero eso es estado operativo cambiante, no memoria durable.
- No metería listas largas de repos candidatos en memoria. Eso pertenece a contexto y specs.
- No metería patrones comunitarios concretos de Telegram/cron/mission control. Son inspiración, no prioridad inmediata.
- No tocaría config permisiva (`approvals.mode: false`, etc.) dentro de esta auditoría porque la restricción explícita pide no aplicar cambios al perfil Hermes.

## Riesgos de la propuesta

- La v1.1 de `MEMORY.md` añade una entrada nueva. Hay que medir tamaño antes de aplicar para mantener el margen bajo el límite aproximado de `2200` caracteres.
- La v1.1 de `USER.md` puede acercarse al límite inyectado de `USER.md`. El archivo actual pesa `1064 B`, pero `prompt-size` reporta `1,401 B` como user profile. Hay que medir tras aplicar.
- La frase “no hacerle repetir información recuperable” puede empujar al agente a buscar demasiado si se interpreta mal. Se mitiga porque `SOUL.md` dice “si puedes recuperarlo”, no “busca indefinidamente”.
- La secuencia read-only → utilidad → loops podría quedarse obsoleta cuando 005 avance. Aun así, como orientación de etapa temprana es útil ahora.

## Recomendación final

### ¿Conviene aplicar esta v1.1 antes de cerrar 004?

**Sí, pero solo si Raúl quiere cerrar 004 con una pequeña mejora de criterio.** No es imprescindible para considerar 004 válido. La versión actual ya cumple la intención estratégica: Hermes dejó de ser genérico y entiende HomeLab.

Mi recomendación pragmática:

1. Si se quiere cerrar 004 hoy: aplicar v1.1 mínima y testear.
2. Si se quiere evitar tocar perfil otra vez: cerrar 004 con estado actual y llevar estas mejoras a una futura iteración de identidad tras uso real.

No haría una reescritura grande.

### ¿Conviene ajustar algo con Raúl antes de aplicarla?

Sí. Dos microdecisiones conviene validarlas con Raúl:

- Si quiere que la preferencia “brainstorming estratégico antes de prompt ejecutivo/spec cerrada” quede como memoria durable de usuario.
- Si la secuencia “repo real read-only antes de loops/canales” debe quedar en `MEMORY.md` o solo en roadmap/specs.

No hace falta una reunión larga. Basta confirmación explícita.

### ¿Qué tests habría que ejecutar si se aplica?

Ejecutaría solo tests pequeños, sin externos:

```bash
wc -c /home/skilland/.hermes/profiles/homelab/SOUL.md \
  /home/skilland/.hermes/profiles/homelab/memories/MEMORY.md \
  /home/skilland/.hermes/profiles/homelab/memories/USER.md

hermes --profile homelab prompt-size

hermes --profile homelab chat --toolsets file,terminal -q "¿Quién eres y cuál es tu papel en Skilland HomeLab? Responde en español, corto y concreto."

hermes --profile homelab chat --toolsets file,terminal -q "Explícame en cristiano qué diferencia hay entre SOUL.md, USER.md, MEMORY.md y AGENTS.md en nuestro setup."

hermes --profile homelab chat --toolsets file,terminal -q "Quiero saltar ya a Telegram, cron y browser. ¿Qué recomiendas hacer primero y por qué?"

hermes --profile homelab chat --toolsets file,terminal -q "Dame directamente un prompt ejecutor para el siguiente microhito estratégico sin debatir nada." 

hermes --profile homelab profile show homelab
pgrep -af "hermes.*gateway" || true
```

Criterios esperados:

- `SOUL.md` sigue razonablemente corto.
- `MEMORY.md` sigue bajo `2200` caracteres aproximados.
- `USER.md` sigue bajo el límite práctico o al menos no crece de forma preocupante en `prompt-size`.
- Hermes responde como Hermes HomeLab, no como asistente genérico.
- Hermes mantiene la partición `SOUL.md` / `USER.md` / `MEMORY.md` / `AGENTS.md`.
- Hermes recomienda primero repo real/read-only/utilidad pequeña antes de Telegram/cron/browser.
- Hermes no entrega sin más un prompt ejecutivo si la petición es estratégica; propone validar marco/tradeoffs.
- `Gateway` sigue parado.
- No aparecen canales externos, cron jobs ni cambios en secrets.

## Bloqueos y unknowns

- Unknown: no se consultó documentación web oficial en vivo; se revisó la documentación oficial cacheada referida por el run 004 y el propio contenido de la spec/run. No hay herramienta web disponible en esta sesión.
- Unknown: no se inspeccionó `.env`, `auth.json`, tokens ni secrets por restricción explícita.
- Unknown: no se verificó si la diferencia entre `USER.md` archivo (`1064 B`) y `prompt-size` user profile (`1,401 B`) tiene implicación práctica real. La trataría como señal de margen, no como fallo.
- Bloqueo deliberado: no se aplicó ningún cambio al perfil Hermes.
- Bloqueo deliberado: no se tocó gateway, cron, skills, browser, MCPs, canales externos, config ni specs.
