# Borrador iterado: blitz HomeLab 22-06 y 23-06

Fecha: 2026-06-21
Estado: borrador de trabajo para planificar mañana; no es spec activa ni output final.

## Idea madre

Salir del bucle "Hermes sobre Hermes".

Hasta ahora HomeLab ha servido para entender Hermes, instalarlo, probarlo, operarlo desde CLI y darle identidad/memoria base. El siguiente tramo debe demostrar que Hermes puede trabajar sobre realidad: repos reales, microhitos pequeños, valor verificable y aprendizaje documentado.

La dirección correcta es:

```text
Hermes trabaja sobre un repo real
-> produce una mejora pequeña
-> se extrae método reusable
-> se prueba continuidad
-> se fijan límites operativos
-> se amplía superficie con cuidado
```

## Principios para este tramo

- No perseguir features de Hermes por entusiasmo.
- No abrir canales externos todavía salvo que haya spec explícita y checklist claro.
- No convertir el blitz en una carrera para tachar microhitos.
- Cada microhito debe dejar aprendizaje usable, no solo documentación para cumplir.
- Primero trabajo real pequeño; después automatización.
- Primero loop manual; después cron, si duele de verdad.
- Primero markdown simple; después kanban, si hace falta.
- Primero política de riesgo; después multi-repo/canales.
- Una skill solo se crea si nace de un patrón real observado, no como demo aspiracional.

## Precondición antes de 005

### Cierre formal de 004 - Hermes identity/memory foundation

Antes de abrir el microhito 005, dejar cerrado y legible el microhito 004:

- confirmar que existe run note de 004;
- confirmar que existe output final de 004;
- confirmar QA contra criterios de aceptación;
- confirmar que `SOUL.md`, `MEMORY.md` y `USER.md` están aplicados al perfil `homelab`;
- confirmar que `02_context/HERMES_RUNTIME_NOTES.md` y `02_context/HERMES_PROFILE_FOUNDATION.md` reflejan el estado real;
- archivar/mover la spec si procede según el harness;
- no iniciar 005 si 004 queda a medio cerrar.

Nota: si 004 ya está materialmente terminada, este bloque debe ser rápido. La idea es no arrancar el siguiente tramo con deuda de cierre.

## Roadmap ajustado 005-013

### Tramo 1 - Hermes trabaja sobre realidad

#### 005 - Hermes first real repo read-only operator

Hermes lee un repo real distinto de HomeLab sin modificar nada.

Objetivo en cristiano:

> Comprobar si Hermes puede aterrizar en un repo real, entenderlo, respetar su contexto y producir criterio útil sin tocar nada.

Entregables esperados:

- mapa operativo del repo;
- qué hace el repo;
- qué estado tiene;
- qué duele;
- riesgos principales;
- deuda visible;
- primer microhito sensato recomendado.

Criterio para elegir repo:

- bajo riesgo;
- sin producción viva;
- sin necesidad de secretos;
- tamaño manejable;
- valor real para Skilland/Reboot;
- preferible si tiene harness o estructura documentable.

Evitar como primer repo:

- CRM;
- sistemas con clientes;
- sistemas con credenciales;
- integraciones externas vivas;
- cualquier repo donde leer ya implique riesgo sensible.

Candidatos probables:

- `google-workspace-CLI-Experiment`;
- `funnel-and-offer-academy`;
- otro repo pequeño si Raúl lo prioriza.

No hacer todavía:

- no escribir archivos;
- no editar specs;
- no instalar dependencias;
- no ejecutar acciones externas;
- no tocar producción;
- no crear skills;
- no automatizar nada.

#### 006 - Primera contribución real pequeña

Pasar de entender a producir algo útil, reversible y verificable en un repo real.

Condición importante:

> 006 debe derivar directamente del diagnóstico de 005. No elegir una tarea abstracta antes de ver qué necesita el repo.

Puede ser:

- crear o mejorar una spec;
- ordenar contexto;
- escribir un output útil;
- cerrar gaps de QA;
- preparar una propuesta concreta;
- hacer un cambio pequeño testeado si el repo lo permite;
- documentar una ruta de operación mínima.

Reglas:

- alcance pequeño;
- reversible;
- verificable;
- sin producción;
- sin secretos;
- sin integraciones externas;
- con QA real al final.

Para qué sirve:

- demostrar que Hermes no solo entiende, sino que aporta valor;
- probar el flujo repo -> contexto -> tarea -> ejecución -> verificación;
- empezar a tratar los repos como fábricas de trabajo.

#### 007 - Primera skill nacida de trabajo real

Extraer una skill mínima a partir de lo aprendido en 005/006.

Condición de entrada:

> Solo crear skill si 005/006 dejan un patrón real repetible. Si no hay patrón claro, se pospone sin drama.

Ejemplos posibles:

- auditar un repo con harness y proponer microhito;
- aterrizar en un repo Skilland;
- cerrar microhito con QA y entregables;
- revisar spec activa y proponer plan realista.

No hacer:

- no crear una skill aspiracional;
- no meter todo el roadmap en una skill;
- no convertir una conversación puntual en SOP permanente.

Resultado sano:

- una skill pequeña, útil, concreta y probada;
- o una decisión explícita de no crear skill todavía porque falta repetición.

### Tramo 2 - Convertir trabajo en sistema

#### 008 - Primer loop aburrido manual

Detectar una rutina repetible antes de automatizarla.

Objetivo en cristiano:

> Encontrar un trabajo aburrido que de verdad se repite y hacerlo manualmente con Hermes antes de meter cron o automatización.

Ejemplos:

- revisar spec activa vs runs/outputs;
- resumir cambios locales;
- detectar trabajo a medias;
- preparar briefing de continuidad;
- revisar estado de varios repos locales sin operar sobre ellos;
- generar un estado rápido del laboratorio.

Regla fuerte:

- aún sin cron;
- aún sin canal externo;
- aún sin loop autónomo;
- primero comprobar que el loop tiene valor manualmente.

#### 009 - Continuidad durable mínima

Crear una forma simple para que el trabajo no muera entre sesiones.

Objetivo:

> Que el HomeLab pueda retomar trabajo sin depender solo del chat o de memoria humana.

Opciones simples:

- cola markdown;
- `CURRENT_STATE.md` o equivalente;
- handoff corto;
- backlog limpio;
- protocolo de reentrada;
- resumen de próximos pasos por repo.

Preferencia:

- empezar con markdown simple;
- no meter kanban oficial si markdown basta;
- no diseñar sistema de gestión antes de sentir la fricción real.

#### 010 - Política operativa de riesgo Hermes HomeLab

Formalizar qué puede hacer Hermes con el perfil `homelab`, especialmente porque quedó en modo de baja fricción.

Contexto real relevante:

```yaml
approvals:
  mode: false
memory:
  write_approval: false
skills:
  write_approval: false
```

Objetivo:

> Mantener velocidad interna sin caer en caos ni abrir superficie sensible sin criterio.

Debe aclarar:

- qué puede hacer Hermes sin preguntar;
- qué debe escalar a Raúl;
- qué sigue prohibido;
- qué cosas están siempre fuera de alcance;
- qué tipos de escritura son aceptables;
- qué tipos de memoria/skill se pueden crear;
- cuándo parar y pedir decisión humana;
- si hace falta un perfil rápido y otro más conservador.

Estilo deseado:

- una página práctica;
- no política enterprise;
- no burocracia;
- sí límites claros.

Razón para poner 010 antes de multi-repo/canales:

> Antes de ampliar superficie, hay que saber qué puede hacer Hermes y dónde debe parar.

### Tramo 3 - Ampliar superficie con cuidado

#### 011 - Primera prueba ligera multi-repo

Cruzar HomeLab + repo real + North Star en una pregunta pequeña.

Objetivo:

- ver si la separación de repos ayuda o empieza a crear fricción;
- conectar visión estratégica con estado operativo;
- detectar qué necesitaría un meta-harness futuro sin diseñarlo todavía.

No objetivo:

- no diseñar meta-harness;
- no crear arquitectura central;
- no crear flota de agentes;
- no resolver multi-repo completo.

Casos sanos:

- North Star + HomeLab;
- HomeLab + repo real;
- visión estratégica + estado operativo de un repo.

Resultado esperado:

- aprendizaje sobre coordinación entre repos;
- límites claros de qué información vive dónde;
- propuesta mínima para futuro multi-repo si hace falta.

#### 012 - Diseño del primer canal humano externo controlado

Diseñar el primer canal externo mínimo, pero no conectarlo todavía por emoción.

Objetivo:

> Preparar la puerta antes de abrirla.

Debe resolver:

- canal candidato: Telegram, WhatsApp u otro;
- por qué ese canal y no otro;
- sandbox;
- allowlist;
- comandos permitidos;
- kill switch;
- logging;
- límites de escritura;
- límites de herramientas;
- qué nunca puede hacer desde canal;
- cómo se prueba sin tocar clientes ni producción.

Regla:

- 012 puede dejar la conexión lista para una spec posterior;
- 012 no tiene que conectar nada;
- si se decide conectar, debería ser otro microhito explícito.

#### 013 - Ejecución del primer canal externo controlado

Solo si 012 pasa QA y Raúl aprueba explícitamente abrir el canal.

Objetivo:

- conectar un canal humano externo mínimo;
- probar una orden inocua;
- recibir un resultado;
- verificar logs, límites, allowlist y kill switch.

No hacer:

- no clientes;
- no producción;
- no CRM/Gmail/Drive;
- no acciones irreversibles;
- no automatización amplia;
- no convertir el canal en mission control completo.

## Secuencia ajustada

```text
004 cierre formal de identidad/memoria
005 repo real read-only
006 contribución pequeña derivada del diagnóstico
007 skill nacida de 005/006, solo si hay patrón real
008 loop aburrido manual
009 continuidad durable mínima en markdown
010 política operativa de riesgo para Hermes HomeLab
011 prueba ligera multi-repo
012 diseño del primer canal humano externo controlado
013 ejecución del primer canal externo, solo si 012 pasa QA y Raúl aprueba
```

## Propuesta realista para 22-06 y 23-06

### 22-06

Objetivo realista:

- cerrar formalmente 004 si falta algo;
- ejecutar 005;
- elegir repo real de bajo riesgo;
- producir diagnóstico read-only;
- si 005 sale limpio, preparar o arrancar 006.

No forzar:

- no forzar skill el mismo día si no hay patrón;
- no saltar a loop/continuidad si aún no hay trabajo real suficiente.

### 23-06

Objetivo realista:

- cerrar 006 con QA real;
- decidir si 007 tiene sentido;
- si hay patrón, crear primera skill;
- si no hay patrón, documentar por qué se pospone;
- empezar 008/009 si ya aparece una rutina repetible o necesidad de continuidad.

Dejar para siguiente tramo si no hay madurez suficiente:

- 010 política;
- 011 multi-repo;
- 012 diseño de canal;
- 013 conexión real.

## Riesgos principales

### Riesgo 1 - Roadmap como checklist de velocidad

El peligro no es el contenido. El peligro es intentar completar 005-013 demasiado rápido.

Mitigación:

- cada microhito debe dejar evidencia real;
- si no hay aprendizaje suficiente, no avanzar por inercia.

### Riesgo 2 - Skill demasiado pronto

Crear skill sin patrón real genera basura procedimental.

Mitigación:

- 007 es condicional;
- si 005/006 no muestran patrón, se pospone.

### Riesgo 3 - Abrir superficie antes de fijar límites

Multi-repo y canal externo son tentadores, pero amplían riesgo.

Mitigación:

- política de riesgo antes de canal externo;
- diseño de canal separado de ejecución;
- aprobación explícita de Raúl para cualquier conexión real.

### Riesgo 4 - Confundir HomeLab con producto cliente

HomeLab puede romper y aprender. Cliente no.

Mitigación:

- no clientes;
- no producción;
- no secretos;
- no CRM/Gmail/Drive/WhatsApp real sin spec específica y aprobación.

## Comentario para el arquitecto de specs

La estructura base es buena y respeta North Star/HomeLab: salir de Hermes sobre Hermes y pasar a trabajo real pequeño.

Ajustes clave incorporados:

- no forzar 005-012 como blitz obligatorio de dos días;
- mover política de riesgo antes del multi-repo/canales;
- separar diseño de canal externo de conexión real;
- hacer 007 condicional a que exista patrón real;
- cerrar formalmente 004 antes de iniciar 005.

## Frase brújula

Después de la fundación de identidad de Hermes, HomeLab debe pasar de configuración a operación real pequeña:

> primero lectura útil, luego contribución real, luego método reusable, luego loop manual, luego continuidad durable, luego límites claros, y solo después multi-repo o canal externo.

## Nota para Hermes / Codex

Este archivo es material de scratch para una sesión posterior. No ejecutar directamente.

Para trabajar mañana:

1. leer este borrador;
2. cerrar formalmente 004 si queda algo pendiente;
3. convertir solo el siguiente microhito en una spec activa dentro de `03_specs/now/`;
4. respetar una sola spec activa;
5. mantener outputs finales en `04_outputs/`;
6. mantener working debris en `05_scratch/`;
7. no abrir canales externos ni tocar producción sin spec y aprobación explícita.
