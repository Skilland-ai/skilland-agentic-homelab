# Hermes self-guided operator onboarding v1

Fecha: 2026-06-21

## Resumen para Raúl

La práctica salió bien: ya sabes abrir, inspeccionar, usar y retomar una sesión básica de Hermes con el perfil `homelab` dentro del repo HomeLab. Hermes sí sirvió como instructor operativo de sí mismo para una primera sesión, siempre que se le pida ir paso a paso, en español y sin trabajo autónomo pesado.

## Qué se practicó

- Preflight mínimo del entorno desde shell.
- Confirmación de repo, binario `hermes`, alias `homelab` y perfil activo.
- Revisión de `profile show` y `config check`.
- Apertura de Hermes CLI con `homelab`.
- Slash commands básicos de inspección y continuidad.
- Lectura local read-only de `02_context/HERMES_RUNTIME_NOTES.md`.
- Cierre con `/quit` y continuidad con `homelab --continue` y `/resume`.
- Cambio posterior de política de aprobaciones por decisión explícita del operador.

## Qué entiende Raúl ahora sobre operar Hermes

- Antes de pedir trabajo, conviene verificar contexto real del repo y del perfil.
- Hermes puede leer contexto local y explicarlo en español sin necesidad de automatización pesada.
- Los slash commands sirven para inspección rápida del runtime, no solo para “chat”.
- La continuidad de sesión existe y puede ser útil, pero también puede arrastrar contexto viejo.
- Que una herramienta aparezca disponible no significa que esté aprobada para usarse en HomeLab.
- El operador puede endurecer o relajar la fricción de aprobaciones desde configuración del perfil.

## Comandos útiles y cuándo usarlos

### Fuera de Hermes

```bash
pwd
git status --short --branch
command -v hermes
command -v homelab || true
hermes --profile homelab profile show homelab
hermes --profile homelab config check
pgrep -af "hermes.*gateway" || true
```

Úsalos para:

- confirmar que estás en el repo correcto;
- ver si hay cambios locales antes de trabajar;
- comprobar que Hermes y el alias funcionan;
- inspeccionar el perfil real;
- revisar warnings de configuración;
- distinguir entre estado declarado y procesos reales del sistema.

### Dentro de Hermes

```text
/profile
/status
/model
/tools list
/toolsets
/memory pending
/skills pending
/save
/title
/quit
/resume
```

Úsalos para:

- comprobar perfil, modelo y estado de sesión;
- ver capacidades visibles;
- revisar si hay pendientes de memoria o skills;
- guardar, titular, salir y retomar sesiones.

## Límites que Hermes reconoció correctamente

Durante la práctica, Hermes reconoció bien estos límites:

- no arrancar Gateway;
- no conectar canales externos;
- no configurar webhooks;
- no configurar cron;
- no usar MCPs externos;
- no usar `--yolo`;
- no tocar sistemas productivos;
- no escribir memoria, skills ni archivos durante el bloque guiado sin aprobación explícita.

## Errores o fricciones observadas

- `config check` produce mucho ruido con variables opcionales irrelevantes para este microhito.
- `profile show` decía `Gateway: stopped`, pero `pgrep` mostró procesos `tui_gateway.*`; eso exige criterio para interpretar el runtime.
- Las aprobaciones manuales se sintieron pesadas para el operador.
- Al configurar `approvals.mode off`, Hermes serializó `approvals.mode: false`, lo que hace recomendable verificar el archivo real o el comportamiento efectivo.

## ¿Hermes sirve como instructor de sí mismo?

Sí, para una primera sesión básica, sí.

Sirve especialmente bien para:

- guiar inspección del entorno;
- explicar qué mirar y por qué;
- leer archivos locales;
- traducir salidas a consecuencias operativas simples.

Sirve peor si:

- el operador quiere velocidad extrema sin prompts;
- el contexto mezcla demasiadas capacidades visibles con políticas aún no definidas;
- se necesita distinguir entre documentación ideal y comportamiento real del runtime.

## Qué falta antes de entrar en memoria y skills

Antes de un microhito centrado en memoria/skills conviene decidir una política clara para `homelab`:

- si seguirá siendo perfil conservador;
- si será perfil rápido sin fricción;
- o si se creará un segundo perfil para pruebas más agresivas.

También conviene resolver o al menos registrar mejor:

- la migración de config pendiente v0 → v30;
- la diferencia entre `Gateway: stopped` y procesos TUI observables;
- una chuleta breve de operación base para futuras sesiones.

## Estado actual del perfil tras esta sesión

Al terminar la conversación, por decisión explícita de Raúl, `homelab` quedó en modo de baja fricción:

```yaml
approvals:
  mode: false
memory:
  write_approval: false
skills:
  write_approval: false
```

Traducción práctica:

- menos prompts o ninguno para aprobaciones;
- memoria escribible sin aprobación;
- skills escribibles sin aprobación.

Esto ya no refleja el modo conservador de la spec 003, sino una preferencia operativa posterior del operador.

## Recomendación del siguiente microhito

Siguiente mejor paso: `004_hermes_profile_memory_skill_lab`.

Pero con un ajuste previo muy recomendable:

- decidir si `homelab` será el perfil rápido “sin fricción total”;
- o si conviene reservar ese modo para otro perfil más desechable y mantener `homelab` algo más controlado.

## Veredicto final

La spec 003 queda completada en lo práctico y ya queda documentada en el repo. Raúl ya sabe pilotar una sesión Hermes básica en HomeLab y ya tiene criterio suficiente para pasar al siguiente microhito, con la salvedad de que ahora el perfil `homelab` quedó más abierto y exigirá más disciplina en los prompts.
