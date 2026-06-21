# Preguntas abiertas

Fecha: 2026-06-21

## Hermes local

- Estado: pendiente de verificar. ¿Está Hermes instalado actualmente en el VPS? No se debe asumir.
- Estado: pendiente de verificar. ¿Qué versión exacta de Hermes se instalará en el primer microhito práctico?
- Estado: pendiente de verificar. ¿Qué proveedor/modelo usará el perfil inicial y con qué presupuesto?
- Estado: pendiente de verificar. ¿Qué modo de instalación conviene para este VPS: CLI-only, Desktop remoto vía dashboard, Docker o entorno Python directo?

## Seguridad

- Estado: pendiente de verificar. ¿Qué directorio de trabajo tendrá el primer perfil Hermes para evitar que opere fuera del HomeLab?
- Estado: pendiente de verificar. ¿Qué approval mode y toolsets serán permitidos en el perfil inicial?
- Estado: pendiente de verificar. ¿Se activarán `memory.write_approval` y `skills.write_approval` desde el inicio?
- Estado: pendiente de verificar. ¿Qué checklist humano autoriza por primera vez un gateway, webhook o MCP externo?

## Relación Codex-Hermes

- Estado: pendiente de verificar. ¿Existe y funciona el preset MCP `codex` en este host?
- Estado: pendiente de verificar. ¿Hermes debe poder disparar tareas Codex-like o solo preparar specs para que Codex las ejecute?
- Estado: pendiente de verificar. ¿Cuál será el contrato de handoff: spec en repo, kanban task, API call o mensaje gateway?

## Operación HomeLab

- Estado: pendiente de verificar. ¿Cuál es el primer loop aburrido que vale automatizar localmente sin canales externos?
- Estado: pendiente de verificar. ¿Se usará kanban oficial desde el inicio o solo después de validar CLI/memoria/skills?
- Estado: pendiente de verificar. ¿Qué información mínima debe entrar en `MEMORY.md` y qué debe quedarse en archivos versionados del repo?
- Estado: pendiente de verificar. ¿Qué criterios convierten una rutina repetida en skill?

## Fuentes comunitarias

- Estado: pendiente de verificar. ¿Qué partes de los hilos/videos se deben contrastar contra código oficial antes de copiarlas?
- Estado: pendiente de verificar. ¿El repo `ClaudioDrews/memory-os` aporta algo reutilizable o solo inspiración?
- Estado: pendiente de verificar. ¿Las claims de precios, versiones y benchmarks comunitarios siguen vigentes?

## Próxima acción propuesta

Estado: pendiente de verificar.

Crear una spec `002_hermes_intimacy_install_smoke_test.md` para instalación controlada y smoke test local: sin gateway externo, sin webhooks, sin MCPs externos, con perfil HomeLab mínimo, setup tipo Blank Slate, memoria/skills con aprobación, `hermes doctor`, primer chat CLI, validación de contexto `AGENTS.md` y run note con logs.
