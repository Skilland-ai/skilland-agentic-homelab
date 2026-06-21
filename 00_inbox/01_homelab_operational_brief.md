# HomeLab Operational Brief Seed — Skilland Agentic HomeLab

**Documento semilla para `00_inbox/`**  
**Repositorio destino previsto:** `skilland-agentic-homelab`  
**Archivo sugerido:** `00_inbox/02_homelab_operational_brief.md`  
**Estado:** brief operativo inicial / microhitos / misión de Codex  
**Fecha:** 2026-06-21  

---

## 0. Propósito de este documento

Este documento define el arranque operativo del repo `skilland-agentic-homelab`.

Debe servir para que Codex, trabajando dentro del VPS y dentro del repo, entienda:

- qué es HomeLab,
- qué estado real tiene el VPS,
- qué filosofía de libertad se aplica,
- qué capacidades se buscan,
- qué primer microhito importa,
- qué papel juega Hermes,
- qué papel juega Codex,
- qué repos pueden entrar después,
- qué debe documentarse,
- y qué decisiones técnicas debe proponer con contexto real.

Este documento no cierra arquitectura.  
Este documento no implementa Hermes.  
Este documento no decide meta-harness.  
Este documento no diseña producto cliente.  

Este documento le da a Codex el mapa de producto y el permiso cultural para empezar a trabajar.

---

## 1. Resumen operativo

El HomeLab es el laboratorio experimental rompible de Skilland/Reboot en el VPS real.

Su misión inmediata es convertir el VPS en un entorno de aprendizaje agentic, con foco inicial en Hermes.

El orden mental inicial:

```text
North Star ya fijó la brújula.
HomeLab empieza el laboratorio.
Codex trabaja dentro del VPS.
Hermes se estudia, instala, toca y rompe.
Los aprendizajes quedan documentados.
Después vendrán repos reales, canales y multi-repo.
```

---

## 2. Estado conocido del VPS

El VPS no es una carpeta local. Es una máquina remota accesible por SSH.

Entrada principal:

```bash
ssh skilland-vps
```

Usuario diario:

```text
skilland
```

Directorio principal para repos:

```bash
/home/skilland/workspaces
```

Codex debe trabajar dentro de un repo concreto ubicado en:

```bash
/home/skilland/workspaces/<repo>
```

No debe trabajarse a diario como root. El alias root existe para administración puntual:

```bash
ssh skilland-vps-root
```

Rutas principales del VPS:

```text
/home/skilland/workspaces   # trabajo diario y repos
/srv/skilland/apps          # apps desplegables
/srv/skilland/services      # servicios residentes o procesos largos
/srv/skilland/data          # datos persistentes no secretos
/srv/skilland/logs          # logs propios del HomeLab
/srv/skilland/backups       # backups locales temporales
/srv/skilland/ops           # runbooks y documentación operativa
/opt/skilland/tools         # herramientas compartidas instaladas manualmente
/etc/skilland               # configuración sensible gestionada por root
```

Tooling base conocido:

```text
git
curl
rsync
jq
rg
tmux
htop
tree
unzip
gcc
make
pipx
docker
docker compose
```

Node/npm/runtimes deben verificarse al arrancar el HomeLab. No se debe asumir stack global definitivo. Codex debe inspeccionar el entorno real y documentar lo que encuentre.

Flujo recomendado de trabajo:

```bash
ssh skilland-vps
cd /home/skilland/workspaces
git clone <repo>
cd <repo>
codex
```

Regla práctica:

- desarrollar dentro de `/home/skilland/workspaces/<repo>`;
- desplegar/operar servicios en `/srv/skilland/apps` o `/srv/skilland/services` cuando toque;
- guardar notas operativas en `/srv/skilland/ops`;
- no confundir la máquina local con el VPS.

---

## 3. Repos iniciales

El repo que debe crearse ahora es:

```text
skilland-agentic-homelab
```

Debe vivir en:

```bash
/home/skilland/workspaces/skilland-agentic-homelab
```

Relación con North Star:

- `skilland-agentic-north-star` es brújula estratégica.
- `skilland-agentic-homelab` es laboratorio operativo.
- HomeLab puede leer y citar North Star, pero no debe modificarla salvo decisión explícita.

---

## 4. Filosofía de permisos

HomeLab funciona en modo **YOLO interno**.

Codex puede trabajar con permisos amplios dentro del VPS y repos autorizados:

- leer,
- escribir,
- crear docs,
- crear notas,
- crear scripts internos,
- instalar o probar piezas cuando el microhito lo requiera,
- proponer estructura,
- ejecutar pruebas,
- documentar errores,
- preparar commits,
- y romper cosas recuperables.

No se debe bloquear el aprendizaje por miedo.

Aun así, acciones con efecto externo real quedan bajo mando explícito de Raúl en el microhito correspondiente:

- enviar emails externos,
- enviar WhatsApps externos,
- tocar clientes,
- publicar,
- borrar irreversible,
- mover secretos,
- cambiar infraestructura crítica,
- tocar producción de CRM o sistemas comerciales reales.

Esto no es una prohibición. Es un protocolo de mando.

---

## 5. Objetivos de capacidad

HomeLab debe explorar capacidades, no carpetas imaginarias.

### 5.1 Hermes Literacy

Entender Hermes conceptualmente:

- qué es,
- qué piezas tiene,
- cómo piensa,
- qué documentación existe,
- qué patrones usa la comunidad,
- qué archivos fundacionales necesita,
- qué conceptos hay que dominar.

### 5.2 Hermes Intimacy

Tocar Hermes en la práctica:

- instalar,
- configurar,
- arrancar,
- parar,
- romper,
- mirar logs,
- observar fallos,
- probar memoria,
- probar agentes,
- probar skills,
- entender runtime.

### 5.3 Codex como operador residente

Consolidar a Codex como el ingeniero que trabaja dentro del repo y del VPS:

- inspecciona,
- propone,
- ejecuta,
- documenta,
- hace QA,
- y eleva decisiones.

### 5.4 Repos como fábricas

Preparar la transición desde repos pasivos a repos operables por agentes.

Primero entender patrones; luego operar repos vivos.

### 5.5 Canales humanos

Más adelante, explorar CLI interno, WhatsApp/Kapso y email/Gmail.

Orden preferente:

1. CLI interno / Codex / Hermes local.
2. Canal humano simple.
3. WhatsApp/email.

### 5.6 Coordinación multi-repo / meta-harness

No diseñar al principio, pero mantenerlo como objetivo de aprendizaje tardío.

### 5.7 Loops reales

No hacer demos vacías. El HomeLab debe terminar probando trabajo real:

- revisar estado de repos,
- operar GWS,
- generar funnel,
- preparar briefing,
- analizar documentos,
- coordinar repos,
- proponer próximos pasos.

---

## 6. Primer microhito: Hermes Deep Research

El primer microhito fuerte es **Hermes Deep Research / Hermes Literacy**.

No debe ir directamente a Gmail, Drive, CRM, WhatsApp, Telegram ni automatizaciones externas.

La prioridad es entender Hermes con profundidad antes de construir encima.

Objetivo:

> Construir conocimiento operativo real sobre Hermes para que deje de ser una herramienta elegida de palabra y empiece a ser un sistema comprendido por Skilland.

Codex debe investigar:

- documentación oficial,
- documentación técnica,
- tutoriales,
- vídeos,
- hilos de Twitter/X,
- repos de referencia,
- ejemplos de setups personales,
- publicaciones de usuarios avanzados,
- patrones del fundador o power users,
- comunidad,
- ejemplos de configuración,
- riesgos,
- límites,
- dependencias,
- y relación con nuestro caso.

Raúl puede añadir fuentes manualmente. Codex también debe buscar, ordenar y proponer fuentes.

Archivo bruto recomendado:

```text
00_inbox/hermes_sources.md
```

Ahí se volcarán links, notas rápidas, vídeos, hilos, repos y comentarios sin necesidad de orden perfecto.

---

## 7. Segundo microhito: Hermes Intimacy

Después de la primera capa de investigación, el siguiente microhito debe tocar Hermes.

Objetivo:

> Instalar, configurar, trastear, romper y observar Hermes en el VPS hasta desarrollar criterio práctico.

Preguntas que debe responder:

- ¿Cómo se instala Hermes?
- ¿Dónde vive?
- ¿Cómo se arranca?
- ¿Cómo se detiene?
- ¿Qué servicios necesita?
- ¿Qué archivos fundacionales usa?
- ¿Cómo maneja memoria?
- ¿Cómo define agentes?
- ¿Cómo maneja skills?
- ¿Cómo registra logs?
- ¿Cómo falla?
- ¿Cómo se recupera?
- ¿Qué espera del entorno?
- ¿Qué relación tiene con repos?
- ¿Qué relación tiene con Codex?

No hace falta terminar con una demo espectacular. El éxito es aprender y documentar.

---

## 8. Tercer microhito: Hermes + Codex relationship

Hipótesis de trabajo inicial:

```text
Hermes coordina, interpreta, enruta y mantiene contexto agentic.
Codex ejecuta microhitos técnicos dentro del VPS/repo.
```

Pero esta relación debe comprobarse en la práctica.

Preguntas:

- ¿Hermes debe dar órdenes a Codex?
- ¿Codex debe preparar piezas para Hermes?
- ¿Hermes es canal/orquestador y Codex ejecutor?
- ¿Dónde acaba uno y empieza el otro?
- ¿Puede Hermes entender el repo HomeLab?
- ¿Puede Codex crear contexto que Hermes use?
- ¿Qué flujo real tiene menos fricción?

Resultado esperado:

- documento vivo `CODEX_AND_HERMES.md`,
- primeras decisiones provisionales,
- preguntas abiertas,
- experimentos sugeridos.

---

## 9. Cuarto microhito: primer repo real

No empezar por CRM si añade demasiada complejidad.

Candidatos preferentes:

1. `google-workspace-CLI-Experiment`
2. `funnel-and-offer-academy`

`basic-scaffolding` puede servir como referencia de harness, pero no debe ser el centro de valor.

Objetivo:

> Que el sistema empiece a entender y operar un repo real con utilidad clara.

Ejemplos de acciones:

- leer instrucciones del repo,
- resumir estado,
- detectar estructura,
- proponer primer caso de uso,
- generar output,
- preparar commit,
- documentar aprendizaje.

---

## 10. Microhito tardío: coordinación multi-repo / meta-harness

El meta-harness interesa y debe permanecer en el horizonte.

No debe resolverse al principio, pero HomeLab debe acabar respondiendo:

- cuándo una petición toca varios repos,
- cómo detectar qué repos intervienen,
- cómo decidir prioridad,
- cómo compartir memoria entre repos,
- cómo evitar duplicación,
- cómo mantener trazabilidad,
- qué forma técnica mínima conviene.

Debe tratarse como aprendizaje avanzado, no como requisito de arranque.

---

## 11. Estructura documental inicial sugerida

Codex puede modificarla si tiene una razón clara, pero una estructura inicial útil sería:

```text
00_inbox/
  01_homelab_foundation_manifesto.md
  02_homelab_operational_brief.md
  hermes_sources.md

01_harness/
  RULES.md
  TASKFLOW.md

02_context/
  PRODUCT_BRIEF.md
  CAPABILITIES.md
  USE_CASES.md
  SUCCESS_CRITERIA.md
  CODEX_MISSION.md
  VPS_STATE.md
  HERMES_LEARNING_NOTES.md
  HERMES_ROLE_IN_HOMELAB.md
  CODEX_AND_HERMES.md
  OPEN_QUESTIONS.md

03_specs/
  now/
  backlog.md

03_runs/
  YYYY-MM-DD_microhito-*.md

04_outputs/

05_ops/
  HERMES_INSTALLATION_NOTES.md
  HERMES_RUNTIME_NOTES.md

05_scratch/
```

Esta estructura no es arquitectura final. Es un punto de partida documental.

---

## 12. Formato ligero de runs

Cada microhito o sesión relevante debe dejar una nota ligera.

Ruta sugerida:

```text
03_runs/YYYY-MM-DD_<microhito>.md
```

Formato:

```markdown
# Run — <nombre>

## Objetivo

## Qué hice

## Qué aprendí

## Qué rompí o qué falló

## Decisiones provisionales

## Preguntas abiertas

## Siguiente paso recomendado
```

No hacerlo oneroso. El objetivo es no perder aprendizaje.

---

## 13. Criterios de éxito del primer bloque

El primer bloque HomeLab será exitoso si:

- el repo `skilland-agentic-homelab` existe y tiene contexto inicial,
- Codex entiende la misión,
- el estado del VPS queda documentado,
- las fuentes Hermes empiezan a ordenarse,
- se procesa documentación de Hermes,
- se inicia o prepara instalación/trasteo,
- hay notas vivas de Hermes,
- se diferencian Hermes Literacy y Hermes Intimacy,
- se documentan preguntas técnicas reales,
- no se cierra arquitectura prematura,
- y Raúl siente que el laboratorio tiene momentum.

---

## 14. Qué evitar al principio

Evitar:

- conectar Gmail/Drive/CRM/WhatsApp demasiado pronto,
- productizar,
- sobrediseñar meta-harness,
- crear seguridad enterprise prematura,
- escribir documentación muerta,
- instalar servicios accesorios sin entender Hermes,
- hacer demos rápidas sin aprendizaje,
- trabajar fuera de repos,
- lanzar Codex en rutas equivocadas,
- confundir VPS con carpeta local,
- asumir Node/npm/runtime sin verificar,
- tocar North Star salvo necesidad estratégica.

---

## 15. Prompt inicial para Codex en el repo HomeLab

Cuando el repo esté creado y estos documentos estén en `00_inbox/`, lanzar Codex dentro de:

```bash
cd /home/skilland/workspaces/skilland-agentic-homelab
codex --yolo
```

Prompt sugerido:

```text
Read all files in 00_inbox/.

You are Codex working inside the Skilland Agentic HomeLab repo on the real VPS.

This repo is the experimental, breakable HomeLab for Skilland/Reboot.

Your mission is not to implement a closed architecture immediately.

Your mission is to initialize the HomeLab context and prepare the first Hermes-focused microhito.

Important principles:

- HomeLab is a YOLO internal lab.
- Hermes is the core target and must be understood deeply.
- Codex is the resident technical operator.
- Do not over-engineer.
- Do not solve meta-harness now.
- Do not connect Gmail/Drive/CRM/WhatsApp yet.
- Start by distilling product/capability context and preparing Hermes Deep Research.
- Document learning.

Tasks:

1. Create or update the minimal repo scaffold if missing:
   - 01_harness/
   - 02_context/
   - 03_specs/now/
   - 03_runs/
   - 04_outputs/
   - 05_ops/
   - 05_scratch/

2. Distill the inbox documents into:
   - 02_context/PRODUCT_BRIEF.md
   - 02_context/CAPABILITIES.md
   - 02_context/USE_CASES.md
   - 02_context/SUCCESS_CRITERIA.md
   - 02_context/CODEX_MISSION.md
   - 02_context/VPS_STATE.md
   - 02_context/HERMES_ROLE_IN_HOMELAB.md
   - 02_context/CODEX_AND_HERMES.md
   - 02_context/OPEN_QUESTIONS.md

3. Create:
   - 00_inbox/hermes_sources.md
   - 03_specs/now/001_hermes_deep_research.md

4. The active spec must define the first microhito:
   Hermes Deep Research / Hermes Literacy.

5. Do not install Hermes yet unless the spec explicitly justifies it as part of the microhito.
   First produce the research plan, source map, and questions.

6. After writing files, print QA:
   - files created,
   - what HomeLab now means,
   - what Hermes research must answer,
   - what remains open,
   - next recommended command or action.
```

Raúl puede modificar el prompt en caliente. El modo YOLO es parte de la cultura del laboratorio.

---

## 16. Decisiones capturadas

1. El repo se llamará `skilland-agentic-homelab`.
2. La naturaleza principal es laboratorio experimental rompible.
3. HomeLab opera con filosofía YOLO interna.
4. Hermes es núcleo objetivo fuerte, no hipótesis débil.
5. Codex es ingeniero residente.
6. Primer bloque fuerte: Hermes Deep Research / Hermes Literacy.
7. Segundo bloque: Hermes Intimacy / instalación y trasteo.
8. Primero CLI/Codex/Hermes; después WhatsApp/email.
9. Primeros repos reales preferentes: GWS CLI y Funnel Academy.
10. Basic Scaffolding sirve como patrón, pero no como principal fuente de valor.
11. Divi es derivada/aprendizaje, no amo del HomeLab.
12. Meta-harness interesa como aprendizaje avanzado, no como primer diseño.

---

## 17. Preguntas abiertas

- ¿Qué fuentes Hermes oficiales y comunitarias son las más importantes?
- ¿Qué documentación debe consumir Codex primero?
- ¿Qué instalación mínima de Hermes conviene en este VPS?
- ¿Qué configuración inicial de Hermes refleja la North Star?
- ¿Cómo se define un agente residente en Hermes?
- ¿Cómo se relaciona Hermes con Codex sin duplicar funciones?
- ¿Cuál será el primer smoke test útil?
- ¿Cuándo se pasa de Hermes Literacy a Hermes Intimacy?
- ¿Qué repo real se toca primero: GWS CLI o Funnel Academy?
- ¿Qué canal humano se conecta primero después del CLI interno?
- ¿Cuándo aparece de verdad la necesidad de meta-harness?
- ¿Qué aprendizajes se etiquetan para Divi?
- ¿Qué partes se quedan solo en laboratorio?

---

## 18. Cierre

El HomeLab debe empezar con energía y claridad.

El primer trabajo no es montar una arquitectura final. El primer trabajo es que Codex y Raúl conviertan el VPS en un laboratorio que aprende, con Hermes como obsesión inicial.

Frase de cierre:

**Antes de pedirle a Hermes que gobierne Skilland, vamos a conocer a Hermes de verdad.**