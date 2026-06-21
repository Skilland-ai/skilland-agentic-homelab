# North Star v0 — Handoff to HomeLab

## Qué es la North Star

Skilland Agentic OS es la visión de una empresa pequeña operable desde la palma de la mano mediante agentes IA residentes que trabajan sobre repos, CRM, Drive, Gmail, GitHub, datos, campañas y entregables reales.

La North Star fija esa ambición sin rebajarla a un bot, un dashboard o una colección de automatizaciones aisladas. El objetivo es una organización agentic que haga trabajo real bajo dirección humana.

## Para qué sirve este repo

Este repo `skilland-agentic-north-star` sirve como compás estratégico del proyecto.

Aquí se definen:

- la visión de largo plazo,
- los principios y anti-principios,
- el macro-faseado,
- las decisiones estratégicas ya tomadas,
- las hipótesis y límites,
- las preguntas que deben resolverse más adelante.

Este repo no es el HomeLab, no es el VPS operativo y no es un espacio para cerrar arquitectura técnica.

## Para qué servirá el repo HomeLab

El futuro repo `skilland-agentic-homelab` será el laboratorio interno y el producto experimental en el VPS real.

Su función será:

- convertir la visión en capacidades explorables,
- probar agentes y flujos reales,
- entender Hermes en contexto,
- operar sobre repos reales,
- descubrir límites,
- documentar aprendizajes,
- transferir lo robusto a Divi-DClick y al camino de productización.

HomeLab debe nacer como espacio de descubrimiento de producto y capacidad, no como arquitectura cerrada desde el día uno.

## Capacidades que HomeLab debe explorar

- VPS como sede viva: que el servidor deje de ser una carpeta suelta y se convierta en una sede operativa entendible.
- Hermes operativo y entendido: comprender su papel real, sus límites y cómo encaja con la North Star.
- Agentes residentes: pasar de respuestas sueltas a agentes con misión, rol y trazabilidad.
- Operación sobre repos reales: leer instrucciones, entender harnesses y producir outputs útiles.
- Coordinación multi-repo: explorar cuándo una petición toca varios repos y qué capacidad superior hace falta.
- Canal humano externo: permitir que Raúl dé órdenes y reciba resultados desde un canal simple.
- Casos de uso reales: priorizar trabajo con valor, no demos vacías.
- Transferencia a Divi-DClick: convertir aprendizaje experimental en algo más sobrio, seguro y vendible.
- Base para productización: detectar módulos, patrones y piezas repetibles para futuros productos o verticales.

## Límites y fronteras

North Star no debe resolver aquí:

- la arquitectura técnica de HomeLab,
- la estructura final del VPS,
- la instalación de Hermes,
- la implementación concreta de Kapso, Gmail, Drive o Calendar,
- el diseño final del meta-harness,
- workers, scripts, servicios, Docker o runtime.

Esas decisiones deben emerger dentro de HomeLab, con contexto real del VPS, repos disponibles, documentación técnica y capacidad de prueba.

## Preguntas que HomeLab debe responder

- ¿Qué capacidades mínimas debe demostrar el laboratorio para considerarse una sede agentic viva?
- ¿Cuál es el primer caso de uso con más valor y menos riesgo?
- ¿Qué primer repo conviene operar de forma real?
- ¿Qué papel real juega Hermes frente a Codex?
- ¿Qué acciones deben requerir aprobación humana desde el inicio?
- ¿Qué parte del aprendizaje debe transferirse a Divi-DClick y qué parte debe quedarse solo en laboratorio?
- ¿Cuándo aparece una necesidad real de coordinación multi-repo?

## Siguiente acción recomendada

Crear el repositorio `skilland-agentic-homelab` y arrancarlo con un documento semilla centrado en:

- capacidades deseadas,
- casos de uso,
- criterios de éxito,
- misión de Codex dentro del VPS,
- estado real del entorno,
- límites y filosofía del laboratorio,
- relación con North Star y con Divi-DClick.