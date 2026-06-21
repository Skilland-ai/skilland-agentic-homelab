# Codex y Hermes

Fecha: 2026-06-21

## Hipótesis práctica

Estado: oficial/verificado.

Codex es el operador técnico dentro del VPS/repo: lee archivos, edita docs/código, ejecuta comandos, verifica outputs y deja trazabilidad en el repositorio. Hermes es candidato a runtime/control layer: mantiene perfiles, memoria, skills, cron, gateway, kanban, dashboard y coordinación persistente.

Estado: pendiente de verificar.

La integración real Codex-Hermes no se probó. No se ejecutó Hermes ni MCP `codex`.

## Cuándo ejecuta Codex

Estado: oficial/verificado para Codex por práctica local del repo; pendiente de verificar para automatización desde Hermes.

Codex debe ejecutar trabajo técnico cuando hace falta manipular este workspace, crear specs, leer código, modificar archivos, correr checks o producir entregables versionables. En el HomeLab actual, Codex sigue siendo la mano técnica confiable porque ya opera dentro del repo.

## Cuándo coordina Hermes

Estado: oficial/verificado.

Hermes debería coordinar cuando la tarea requiere memoria entre sesiones, rutinas recurrentes, perfiles especializados, colas kanban, skills como SOPs, gateway o triggers. Hermes no reemplaza a Codex para edición técnica profunda hasta que una integración esté probada.

## Cómo Codex prepara contexto para Hermes

Estado: oficial/verificado.

Codex puede preparar los archivos que Hermes leerá después: `AGENTS.md`, specs en `03_specs/`, contexto en `02_context/`, outputs en `04_outputs/`, run notes en `03_runs/` y skills si una spec lo exige. Este repo ya tiene harness, taskflow y QA, así que Codex puede convertir investigación en memoria operativa para un futuro perfil Hermes.

## Futuro: Hermes dispara trabajo tipo Codex

Estado: pendiente de verificar.

La documentación oficial menciona MCPs, preset `codex`, API server, ACP y herramientas de terminal. La hipótesis futura es que Hermes pueda recibir un evento, crear/coordinar una tarea y disparar trabajo técnico en una herramienta tipo Codex. Antes de hacerlo en Skilland hay que probarlo en un repo dummy, con toolsets limitados, sin secretos y con aprobación humana.

## Frontera operativa

Estado: oficial/verificado.

- Codex: ejecución puntual, edición, verificación, entrega.
- Hermes: memoria, coordinación, scheduling, perfiles, colas, gateway y observabilidad.
- Repo HomeLab: contrato común entre ambos.
- Specs: mecanismo de seguridad para no improvisar.

## Riesgos

Estado: pendiente de verificar.

- Duplicar memoria entre Codex, Hermes y archivos del repo.
- Permitir a Hermes tocar demasiado filesystem sin límites.
- Conectar gateway antes de tener allowlists y auditoría.
- Crear perfiles "departamento" antes de tener procesos repetibles.
- Confundir dashboard con producto final.

## Decisión propuesta

Estado: pendiente de verificar.

Mantener Codex como operador técnico principal durante los próximos microhitos. Introducir Hermes primero como runtime local controlado, lector del repo y ejecutor de pruebas pequeñas. Solo después probar coordinación Hermes -> tarea técnica, y siempre en entorno no productivo.
