# 001 Hermes Deep Research / Hermes Literacy

## Resultado
- Debe existir un research pack estructurado, útil y accionable sobre Hermes para Skilland Agentic HomeLab.
- Este microhito convierte `00_inbox/hermes_sources.md` y las fuentes oficiales de Hermes en contexto operativo.
- La ejecución debe terminar con una recomendación clara del siguiente microhito.

## Modo De Trabajo
- Esta spec será ejecutada por una sesión implementadora posterior.
- Esta sesión arquitecta define la spec y podrá evaluar después los resultados contra criterios de aceptación.
- Todo output generado por la sesión implementadora debe estar en español.
- Se permiten nombres técnicos, rutas, comandos, URLs, claves de configuración y títulos originales en inglés cuando sea necesario.

## Archivos A Leer Primero
Leer en este orden antes de escribir:

1. `AGENTS.md`
2. `01_harness/RULES.md`
3. `01_harness/STACK.md`
4. `01_harness/TASKFLOW.md`
5. Todos los archivos de `02_context/`
6. Esta spec activa en `03_specs/now/001_hermes_deep_research.md`
7. `00_inbox/hermes_sources.md`

## Objetivo
Entender Hermes con profundidad antes de instalar, configurar o construir encima.

La investigación debe priorizar documentación oficial y repositorio oficial como fuentes de verdad técnica, y usar fuentes comunitarias como inspiración para setups, playbooks, configuraciones, workflows, operator mindset y metagame.

## Alcance
- Crear un mapa procesado de fuentes Hermes.
- Sintetizar aprendizaje oficial y comunitario.
- Definir una primera hipótesis del rol de Hermes en HomeLab.
- Definir una primera hipótesis práctica de convivencia Codex + Hermes.
- Crear un glosario específico de conceptos Hermes.
- Crear una síntesis ejecutiva para Raúl.
- Crear run note con fuentes, aprendizajes, riesgos, QA y siguiente acción.
- Actualizar preguntas abiertas específicas de Hermes.

## Fuera De Alcance
- No instalar Hermes.
- No configurar servicios productivos.
- No conectar Gmail.
- No conectar Drive.
- No conectar CRM.
- No conectar WhatsApp.
- No conectar Kapso.
- No conectar Telegram.
- No conectar Slack.
- No conectar Discord.
- No conectar sistemas externos.
- No diseñar el meta-harness final.
- No construir Mission Control.
- No tocar producción ni sistemas comerciales reales.

## Fuentes Prioritarias
- Fuente oficial primaria: `https://hermes-agent.nousresearch.com/docs`
- Indice oficial para agentes: `https://hermes-agent.nousresearch.com/docs/llms.txt`
- Repositorio oficial: `https://github.com/NousResearch/hermes-agent`
- Dump bruto de Raul: `00_inbox/hermes_sources.md`

Reglas de fuente:
- Tratar documentación oficial y repositorio oficial como verdad técnica prioritaria.
- Tratar hilos de X/Twitter, transcripciones, setups comunitarios, videos, articulos y notas de power users como fuentes secundarias.
- No presentar una afirmacion comunitaria como verdad tecnica si no esta confirmada en documentacion oficial o codigo fuente.
- Si una fuente no se revisa realmente, marcarla como pendiente.
- Preservar intacto `00_inbox/hermes_sources.md`.

## Entregables
- `02_context/HERMES_SOURCE_MAP.md`
- `02_context/HERMES_LEARNING_NOTES.md`
- `02_context/HERMES_ROLE_IN_HOMELAB.md`
- `02_context/CODEX_AND_HERMES.md`
- `02_context/HERMES_CONCEPTS_GLOSSARY.md`
- `02_context/OPEN_QUESTIONS.md`
- `04_outputs/2026-06-21_hermes_metagame_initial_synthesis.md`
- `03_runs/2026-06-21_hermes_deep_research_run_01.md`

## Contenido Esperado Por Entregable

### `02_context/HERMES_SOURCE_MAP.md`
Debe clasificar fuentes en:
- fuentes oficiales / primarias;
- repositorio oficial / referencias de codigo fuente;
- fuentes comunitarias de setup/playbook;
- videos/tutoriales;
- hilos de X/Twitter;
- inspiracion / metagame;
- pendientes de revisar;
- revisadas;
- necesitan verificacion contra docs oficiales.

Para cada fuente, incluir:
- titulo o nombre corto;
- URL;
- tipo;
- prioridad;
- estado de revision;
- para que parece util;
- si necesita verificacion oficial.

### `02_context/HERMES_LEARNING_NOTES.md`
Debe explicar que se entiende sobre Hermes tras la investigacion.

Cubrir al menos:
- que es Hermes;
- por que no es solo un chatbot;
- relacion entre CLI, Desktop y Gateway;
- profiles/perfiles;
- `SOUL.md`;
- `MEMORY.md`;
- `USER.md`;
- archivos de contexto de proyecto como `AGENTS.md`;
- skills;
- cron jobs;
- `/goal`;
- slash commands;
- sub-agents / delegation;
- kanban;
- gateway y superficies de mensajeria;
- Telegram/workspaces/topics;
- webhooks/event triggers;
- mission control/dashboard;
- MCPs/tool integrations;
- API server;
- IDE/ACP integration;
- profile distributions;
- memoria/wiki/Obsidian-style knowledge base;
- controles de coste/token como `no_agent`, `wakeAgent`, `context_from`, toolsets ligeros y modelo por tarea.

Etiquetar cada bloque como:
- `oficial/verificado`;
- `comunitario/no verificado`;
- `pendiente de verificar`.

### `02_context/HERMES_ROLE_IN_HOMELAB.md`
Debe explicar la primera hipotesis de trabajo sobre Hermes en Skilland HomeLab.

Debe abordar:
- Hermes como nucleo objetivo del HomeLab;
- Hermes como capa operativa, no simple chat;
- Hermes como posible control room/orquestador;
- perfiles como posibles departamentos o agentes especialistas;
- skills como SOPs/procedimientos reutilizables;
- cron/webhooks como loops/triggers;
- kanban/mission control como capa de visibilidad;
- por que empezamos con literacy antes de instalar/construir;
- que no debe sobreconstruir HomeLab todavia.

### `02_context/CODEX_AND_HERMES.md`
Debe definir una hipotesis practica, no arquitectura final.

Debe abordar:
- Codex como operador tecnico residente dentro del VPS/repo;
- Hermes como runtime/capa agentic/control layer;
- cuando Codex debe ejecutar trabajo tecnico de repo/VPS;
- cuando Hermes debe coordinar, recordar, enrutar u operar como asistente;
- como Codex puede preparar contexto, archivos, specs y documentacion para Hermes;
- como Hermes podria mas adelante disparar trabajo tipo Codex;
- que sigue siendo desconocido.

### `02_context/HERMES_CONCEPTS_GLOSSARY.md`
Debe definir en español:
- Hermes;
- Hermes Desktop;
- CLI;
- Gateway;
- Profile;
- `SOUL.md`;
- `MEMORY.md`;
- `USER.md`;
- `AGENTS.md`;
- Skill;
- Curator;
- Cron;
- `no_agent`;
- `wakeAgent`;
- `context_from`;
- `/goal`;
- `/subgoal`;
- `/background`;
- `/queue`;
- `/steer`;
- `delegate_task`;
- Sub-agent;
- Kanban;
- Mission Control;
- MCP;
- API server;
- ACP / IDE integration;
- Profile distribution;
- Toolsets;
- Memory loop;
- Compression;
- Wiki / knowledge base.

### `04_outputs/2026-06-21_hermes_metagame_initial_synthesis.md`
Sintesis en español para Raul.

Debe responder:
- cual es el metagame actual de Hermes segun las fuentes;
- que dicen las fuentes oficiales frente a las fuentes comunitarias;
- cuales son los patrones de mas leverage;
- que deberia copiar Skilland;
- que deberia evitar Skilland;
- cual es el camino de aprendizaje recomendado;
- cuales son los primeros 3 microhitos despues de esta investigacion;
- que no debemos construir todavia;
- cuales son las ideas mas potentes para HomeLab.

Estilo:
- practico;
- accionable;
- cero academicismo;
- cero humo;
- separando oficial vs comunidad.

### `03_runs/2026-06-21_hermes_deep_research_run_01.md`
Debe incluir:
- objetivo;
- archivos fuente leidos;
- fuentes oficiales revisadas;
- fuentes comunitarias revisadas;
- fuentes pendientes;
- principales aprendizajes;
- riesgos;
- decisiones propuestas;
- preguntas abiertas;
- siguiente accion recomendada;
- QA explicito contra todos los criterios de aceptacion.

## Plan De Ejecucion
1. Hacer preflight:
   - calcular checksum de `00_inbox/hermes_sources.md`;
   - confirmar que `00_inbox/hermes_sources.md` no se modifica;
   - crear `03_runs/` si falta;
   - comprobar estado inicial con `git status --short`.
2. Revisar documentacion oficial:
   - instalacion;
   - CLI;
   - perfiles;
   - contexto;
   - memoria;
   - skills;
   - curator;
   - cron;
   - delegation;
   - kanban;
   - goals;
   - gateway;
   - messaging;
   - webhooks;
   - MCP;
   - API server;
   - ACP;
   - toolsets;
   - security.
3. Revisar el repositorio oficial solo para confirmar estructura o codigo cuando las docs no basten.
4. Procesar `00_inbox/hermes_sources.md` fuente por fuente.
5. Clasificar cada fuente por tipo, prioridad, estado, utilidad y necesidad de verificacion.
6. Escribir documentos de `02_context/` en español.
7. Escribir sintesis ejecutiva en `04_outputs/`.
8. Escribir run note en `03_runs/`.
9. Recalcular checksum de `00_inbox/hermes_sources.md`.
10. Registrar QA final en la run note y en el mensaje final.

## Criterios De Aceptacion
- [ ] Existe `02_context/HERMES_SOURCE_MAP.md`.
- [ ] Existe `02_context/HERMES_LEARNING_NOTES.md`.
- [ ] Existe `02_context/HERMES_ROLE_IN_HOMELAB.md`.
- [ ] Existe `02_context/CODEX_AND_HERMES.md`.
- [ ] Existe `02_context/HERMES_CONCEPTS_GLOSSARY.md`.
- [ ] Existe `04_outputs/2026-06-21_hermes_metagame_initial_synthesis.md`.
- [ ] Existe `03_runs/2026-06-21_hermes_deep_research_run_01.md`.
- [ ] `02_context/OPEN_QUESTIONS.md` incluye preguntas abiertas especificas de Hermes.
- [ ] `00_inbox/hermes_sources.md` queda intacto segun checksum antes/despues.
- [ ] No se conectaron sistemas externos.
- [ ] No se tocaron sistemas productivos.
- [ ] Todo output generado esta en español salvo URLs, comandos, rutas, claves tecnicas, nombres propios o citas necesarias.
- [ ] Las afirmaciones tecnicas estan etiquetadas como `oficial/verificado`, `comunitario/no verificado` o `pendiente de verificar`.
- [ ] La siguiente accion recomendada queda clara.

## QA Final Esperado
El mensaje final de la sesion implementadora debe incluir, en español:
- archivos creados/actualizados;
- fuentes revisadas;
- fuentes pendientes;
- que quedo verificado por fuentes oficiales;
- que queda como comunidad/no verificado;
- principales aprendizajes sobre Hermes;
- riesgos;
- microhito recomendado despues;
- si la spec activa queda completada o necesita otra ronda de research.

## Riesgos
- Riesgo: mezclar afirmaciones comunitarias con verdad tecnica oficial.
- Riesgo: crear documentos demasiado largos y poco utiles.
- Riesgo: empezar a instalar o conectar canales antes de terminar literacy.
- Riesgo: descargar clones o dumps grandes dentro del repo.
- Riesgo: afirmar haber revisado fuentes que solo fueron detectadas.

## Open Questions
- Que partes de Hermes estan suficientemente verificadas por documentacion oficial para pasar a instalacion controlada.
- Que claims comunitarios merecen verificacion posterior en codigo fuente.
- Que primer smoke test tendria mas valor para Hermes Intimacy.
- Que rol inicial conviene para un primer profile de HomeLab.
- Que permisos/herramientas deben estar apagados por defecto en una instalacion inicial segura.

## Siguiente Accion Recomendada
Ejecutar esta spec en una nueva sesion implementadora enfocada solo en investigacion Hermes Literacy.
