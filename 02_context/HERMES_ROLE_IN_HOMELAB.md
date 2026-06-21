# Rol de Hermes en el HomeLab Skilland

Fecha: 2026-06-21

## Hipótesis principal

Estado: oficial/verificado.

Hermes puede ser el núcleo operativo del HomeLab porque combina agente interactivo, memoria, skills, cron, gateway, kanban, perfiles, dashboard, MCPs y API en un mismo runtime. No es solo una interfaz de chat; es una capa donde se pueden modelar operaciones recurrentes con estado.

Estado: pendiente de verificar.

Todavía no se ha instalado ni ejecutado Hermes en este VPS dentro de una spec controlada. Por lo tanto, esta hipótesis es de rol y arquitectura, no de operación ya probada.

## Nucleo HomeLab

Estado: oficial/verificado.

Como núcleo, Hermes debería empezar con un perfil interno de laboratorio, no con canales externos. Ese perfil puede leer contexto del repo, respetar `AGENTS.md`, tener `SOUL.md` mínimo, memoria con aprobación y toolsets limitados. La primera validación debe ser aburrida: CLI, modelo, contexto, una tarea pequeña y logs claros.

## Capa operativa y sala de control

Estado: oficial/verificado.

El dashboard oficial y kanban oficial ya dan piezas de sala de control: perfiles, sesiones, logs, memoria, cron, skills, webhooks, MCPs y estado de tareas. Para Skilland, "Mission Control" no debe empezar como app custom; debe empezar como observación disciplinada de lo que Hermes ya expone.

Estado: comunitario/no verificado.

Los hilos comunitarios empujan la idea de un control room con Telegram topics, dashboards y triggers. La idea es fuerte, pero copiarla demasiado pronto produciría teatro de control sin operación real.

## Perfiles como departamentos

Estado: oficial/verificado.

Los perfiles pueden representar funciones: research, ops, code, editorial, QA. Cada uno puede tener personalidad, skills, cron y memoria propios. En HomeLab esto encaja con "departamentos" internos, pero hay que recordar que un perfil no limita filesystem por sí mismo.

Decisión propuesta: comenzar con un solo perfil HomeLab y crear especialistas solo cuando exista una rutina real que lo justifique.

## Skills como SOPs

Estado: oficial/verificado.

Las skills son la forma natural de convertir procedimientos repetidos en SOPs vivos. Para Skilland, una skill debería nacer solo después de ejecutar manualmente una rutina varias veces y saber qué verificación exige. No conviene llenar `skills/` con aspiraciones.

## Cron y webhooks como loops y triggers

Estado: oficial/verificado.

Cron sirve para loops recurrentes. Webhooks sirven para eventos externos. `no_agent`, `wakeAgent` y `context_from` permiten bajar costo y despertar al agente solo cuando hay cambio. Esto encaja con operaciones tipo investigación diaria, vigilancia de repos, digest de métricas o QA programado.

Restricción: no activar webhooks ni canales externos hasta tener seguridad, secretos, allowlists y objetivo concreto.

## Kanban y visibilidad

Estado: oficial/verificado.

Kanban aporta durabilidad, cola y handoffs. Es mejor que subagentes para trabajo que debe sobrevivir interrupciones y tener historial. En HomeLab puede ser el puente entre intención humana, workers Hermes y revisión de Raúl.

## Alfabetización antes de instalación

Estado: oficial/verificado.

La documentación oficial recomienda empezar con setup simple y una sesión CLI limpia antes de capas avanzadas. La spec actual acierta al exigir alfabetización previa: evita confundir posibilidades con capacidades ya dominadas.

## Lo que no se debe sobreconstruir

Estado: comunitario/no verificado.

No copiar todavía: mission control custom, flotas de perfiles, Telegram workspaces, webhooks productivos, memoria Obsidian compleja, agentes "departamento" para cada idea, ni integraciones con CRM/Gmail/Drive/WhatsApp.

Estado: oficial/verificado.

Los mecanismos existen, pero cada uno añade estado, permisos y superficie de fallo. El HomeLab debe instalar primero, observar, romper en pequeño, documentar y solo después automatizar.

## Rol inicial recomendado

Estado: pendiente de verificar.

Hermes debería entrar en Skilland como "residente de laboratorio" local: un perfil conectado al repo HomeLab, sin canales externos, sin servicios productivos, con memoria y skills bajo aprobación. Cuando ese residente demuestre estabilidad, se puede promover a coordinador de loops internos.
