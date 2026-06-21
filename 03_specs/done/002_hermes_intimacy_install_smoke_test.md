# 002 Hermes Intimacy / Install + Smoke Test Local

Estado: archivada despues de ejecucion y revision humana el 2026-06-21.

## Resultado
- Hermes queda instalado o verificado en el VPS como usuario `skilland`.
- Existe un perfil local `homelab` para pruebas controladas del HomeLab.
- Se ejecuta un smoke test local de CLI/chat que lee contexto del repo sin modificar archivos.
- Quedan documentados comandos, salidas sanitizadas, fallos, riesgos y siguiente microhito.

## Archivos A Leer Primero
Leer en este orden antes de escribir o ejecutar:

1. `AGENTS.md`
2. `01_harness/RULES.md`
3. `01_harness/STACK.md`
4. `01_harness/TASKFLOW.md`
5. Todos los archivos de `02_context/`
6. Esta spec activa: `03_specs/now/002_hermes_intimacy_install_smoke_test.md`
7. Run previo: `03_runs/2026-06-21_hermes_deep_research_run_01.md`
8. Output previo: `04_outputs/2026-06-21_hermes_metagame_initial_synthesis.md`

## Objetivo
Pasar de Hermes Literacy a Hermes Intimacy mínima: instalar o verificar Hermes, configurar autenticación persistente, crear un perfil local de laboratorio y validar que Hermes puede entender este repo mediante una tarea inocua.

Este microhito no busca operar el HomeLab todavía. Busca comprobar que el runtime arranca, diagnostica, se autentica, lee contexto local y puede responder de forma verificable.

## Alcance
- Verificar estado real del VPS y prerequisitos.
- Instalar Hermes per-user si no existe.
- Configurar autenticación persistente de modelo.
- Crear perfil `homelab` sin skills bundled.
- Configurar mínimos de seguridad para el perfil.
- Ejecutar `hermes doctor`, `hermes status`, `hermes profile show homelab` y un primer chat local.
- Documentar resultados en contexto, run note y output final.

## Fuera De Alcance
- No usar root para trabajo diario.
- No usar `sudo` salvo que el instalador indique explícitamente un prerequisito externo y se documente como bloqueo, no como acción automática.
- No usar `--yolo`.
- No arrancar Gateway.
- No conectar Telegram.
- No conectar WhatsApp.
- No conectar Gmail.
- No conectar Drive.
- No conectar CRM.
- No conectar Kapso.
- No conectar Slack.
- No conectar Discord.
- No configurar webhooks.
- No configurar MCPs externos.
- No exponer dashboard públicamente.
- No tocar sistemas productivos.
- No crear perfiles múltiples ni agentes especialistas.
- No crear skills reales todavía.
- No programar cron jobs.

## Fuentes Oficiales A Usar
- `https://hermes-agent.nousresearch.com/docs`
- `https://hermes-agent.nousresearch.com/docs/llms.txt`
- `05_scratch/hermes_official/docs/getting-started__installation.md`
- `05_scratch/hermes_official/docs/getting-started__quickstart.md`
- `05_scratch/hermes_official/docs/user-guide__configuration.md`
- `05_scratch/hermes_official/docs/user-guide__security.md`
- `05_scratch/hermes_official/docs/reference__cli-commands.md`
- `05_scratch/hermes_official/docs/reference__profile-commands.md`

Si el cache oficial en `05_scratch/hermes_official/` no existe o parece obsoleto, consultar las URLs oficiales directamente. No clonar dumps grandes dentro del repo.

## Estado Inicial Esperado
En la planificación previa se observó:
- `hermes` no estaba en `PATH`.
- `~/.hermes` no existía.
- `node`, `npm`, `python3`, `pipx` y `docker` estaban disponibles.
- No había variables de entorno visibles para proveedores LLM.

La sesión ejecutora debe verificar de nuevo estos datos. Si han cambiado, documentar el estado real y actuar según esta spec.

## Política De Autenticación
- Opción principal: usar OAuth persistente de Nous Portal mediante el flujo oficial de Hermes (`hermes model` o wizard oficial equivalente).
- Si Nous Portal no está disponible, usar una API key persistente aportada por Raúl durante la sesión y configurada mediante flujo oficial de Hermes.
- Nunca escribir claves, tokens, device codes ni secretos en archivos del repo, run notes, outputs o chat final.
- Si Raúl no puede completar login/auth, marcar el microhito como `blocked: auth` después de instalar/verificar Hermes y completar diagnósticos posibles.

## Entregables
- `02_context/HERMES_RUNTIME_NOTES.md`
- `04_outputs/2026-06-21_hermes_intimacy_install_smoke_test_v1.md`
- `03_runs/2026-06-21_hermes_intimacy_install_smoke_test_run_01.md`

Material temporal permitido:
- `05_scratch/hermes_install/`

## Plan De Ejecución

### 1. Preflight
Ejecutar y registrar salidas sanitizadas:

```bash
pwd
whoami
hostname
git status --short
command -v hermes || true
test -d "$HOME/.hermes" && echo "HERMES_HOME_EXISTS" || echo "HERMES_HOME_MISSING"
git --version
curl --version | head -1
xz --version | head -1 || true
node --version || true
npm --version || true
python3 --version || true
pipx --version || true
docker --version || true
```

Reglas:
- Si `~/.hermes` existe pero `hermes` no está en `PATH`, no instalar encima. Documentar bloqueo porque podría haber instalación parcial o credenciales previas.
- Si `hermes` existe, no reinstalar. Saltar a verificación.

### 2. Instalación Per-User
Si `hermes` no existe y `~/.hermes` no existe:

```bash
mkdir -p 05_scratch/hermes_install
curl -fsSL https://hermes-agent.nousresearch.com/install.sh -o 05_scratch/hermes_install/install.sh
sed -n '1,180p' 05_scratch/hermes_install/install.sh
bash 05_scratch/hermes_install/install.sh --skip-browser
export PATH="$HOME/.local/bin:$PATH"
```

Reglas:
- No ejecutar el instalador con root.
- No usar `sudo`.
- Si el instalador pide setup interactivo, elegir ruta mínima/controlada. Preferir modo `Blank Slate` si aparece como opción.
- Si el instalador falla por dependencia del sistema que requiere root, parar y documentar el comando recomendado por Hermes como bloqueo.

### 3. Verificación Base
Ejecutar:

```bash
export PATH="$HOME/.local/bin:$PATH"
command -v hermes
hermes version
hermes doctor
hermes status
```

Reglas:
- Sanitizar salidas antes de copiarlas a documentos.
- No incluir rutas con secretos ni tokens.
- Si `hermes doctor` falla, documentar diagnóstico y no avanzar a perfil/chat hasta resolver o marcar bloqueo.

### 4. Autenticación Persistente
Configurar proveedor/modelo con el flujo oficial:

```bash
hermes model
```

Decisiones:
- Prioridad: Nous Portal OAuth.
- Fallback: API key persistente aportada por Raúl.
- No usar variables efímeras como solución principal.
- No pegar secretos en Markdown.

Verificar después:

```bash
hermes status
hermes doctor
```

Si no hay autenticación usable, registrar `blocked: auth` y completar documentos con lo conseguido.

### 5. Perfil Local `homelab`
Crear perfil si no existe:

```bash
hermes profile list
hermes profile create homelab --no-skills --description "Perfil local de laboratorio para Skilland Agentic HomeLab."
hermes profile show homelab
```

Si el perfil ya existe:
- No borrarlo.
- Mostrarlo con `hermes profile show homelab`.
- Documentar si fue creado antes.

Configurar mínimos:

```bash
hermes --profile homelab config set terminal.cwd /home/skilland/workspaces/skilland-agentic-homelab
hermes --profile homelab config set approvals.mode manual
hermes --profile homelab config set memory.write_approval true
hermes --profile homelab config set skills.write_approval true
```

Notas:
- No asumir que el perfil es sandbox de filesystem.
- Para el smoke test, limitar herramientas por invocación con `--toolsets file,terminal`.
- No habilitar toolsets web/browser/messaging/cron/MCP para este microhito.

### 6. Smoke Test Local
Ejecutar desde el repo:

```bash
cd /home/skilland/workspaces/skilland-agentic-homelab
hermes --profile homelab chat --toolsets file,terminal -q "Lee AGENTS.md y README.md de este repo sin modificar archivos. Responde en español con 5 bullets: qué es el repo, qué no debes hacer, cuál es la spec activa, qué sistemas externos están fuera de alcance y qué comando usarías para ver el estado git."
```

El resultado debe demostrar:
- Responde en español.
- Identifica el repo como Skilland Agentic HomeLab.
- Reconoce la spec activa `002_hermes_intimacy_install_smoke_test`.
- Dice que no debe conectar sistemas externos.
- Propone `git status --short` o equivalente para revisar estado git.
- No modifica archivos.

Si el chat falla por auth, modelo o provider, documentar el fallo exacto sin secretos y marcar bloqueo.

### 7. Verificación De No Alcance
Comprobar y registrar:

```bash
pgrep -af "hermes.*gateway" || true
hermes profile show homelab
git status --short
```

Confirmar explícitamente:
- No se arrancó Gateway.
- No se conectaron canales externos.
- No se configuraron webhooks.
- No se configuraron MCPs externos.
- No se tocó producción.
- No se usó `--yolo`.

## Contenido Esperado Por Entregable

### `02_context/HERMES_RUNTIME_NOTES.md`
Debe incluir:
- estado real de instalación;
- versión de Hermes;
- ubicación del binario;
- estado de `~/.hermes`;
- perfil `homelab`;
- configuración segura aplicada;
- estado de auth sin secretos;
- resultado de `doctor`;
- resultado del smoke test;
- limitaciones y bloqueos.

### `04_outputs/2026-06-21_hermes_intimacy_install_smoke_test_v1.md`
Debe ser una síntesis para Raúl:
- qué se instaló o verificó;
- qué funcionó;
- qué falló;
- qué aprendimos de Hermes en ejecución real;
- si Hermes está listo para el microhito 003;
- riesgos antes de activar memoria/skills/cron;
- siguiente recomendación.

### `03_runs/2026-06-21_hermes_intimacy_install_smoke_test_run_01.md`
Debe incluir:
- objetivo;
- comandos ejecutados;
- salidas sanitizadas;
- decisiones tomadas;
- errores y fixes;
- bloqueos;
- QA contra criterios de aceptación;
- `git status --short` inicial y final;
- siguiente acción recomendada.

## Criterios De Aceptación
- [ ] Existe `02_context/HERMES_RUNTIME_NOTES.md`.
- [ ] Existe `04_outputs/2026-06-21_hermes_intimacy_install_smoke_test_v1.md`.
- [ ] Existe `03_runs/2026-06-21_hermes_intimacy_install_smoke_test_run_01.md`.
- [ ] `hermes` está instalado o su ausencia queda documentada con bloqueo accionable.
- [ ] `hermes version` queda registrado si `hermes` está disponible.
- [ ] `hermes doctor` queda registrado si `hermes` está disponible.
- [ ] La autenticación queda persistente o se marca `blocked: auth` sin exponer secretos.
- [ ] Existe o queda documentado el perfil `homelab`.
- [ ] El perfil `homelab` tiene `terminal.cwd` apuntando al repo.
- [ ] El perfil `homelab` tiene `approvals.mode` en `manual`.
- [ ] El perfil `homelab` tiene `memory.write_approval` en `true`.
- [ ] El perfil `homelab` tiene `skills.write_approval` en `true`.
- [ ] El smoke test local se ejecuta correctamente o queda bloqueado por auth/provider con causa concreta.
- [ ] No se usa root para trabajo diario.
- [ ] No se usa `sudo` salvo para documentar un bloqueo, no para ejecutarlo.
- [ ] No se usa `--yolo`.
- [ ] No se arranca Gateway.
- [ ] No se conectan canales externos.
- [ ] No se configuran webhooks.
- [ ] No se configuran MCPs externos.
- [ ] No se tocan sistemas productivos.
- [ ] `00_inbox/hermes_sources.md` no se modifica.
- [ ] `git status --short` final no muestra cambios inesperados fuera de spec, scratch y entregables.
- [ ] La siguiente acción recomendada queda clara.

## Riesgos
- El instalador oficial puede requerir dependencias del sistema no disponibles sin root.
- El flujo OAuth puede requerir intervención humana y bloquear el chat si no se completa.
- El backend local de terminal no aísla filesystem; el perfil no es sandbox.
- `hermes-cli` puede traer más herramientas de las deseadas por defecto; para el smoke test se limita con `--toolsets file,terminal`.
- Salidas de diagnóstico podrían contener rutas o datos sensibles; deben sanearse antes de documentar.

## Open Questions
- ¿Qué provider/modelo quedará como default real para HomeLab?
- ¿El perfil `homelab` debe mantener backend local o pasar a Docker en el microhito 003?
- ¿Conviene activar memoria y skills bajo aprobación en 003 o probar primero solo una sesión más larga?
- ¿Qué primer procedimiento real merece convertirse en skill?

## Siguiente Acción Recomendada
Si esta spec pasa, planificar `003_hermes_profile_memory_skill_lab`: primer `SOUL.md` HomeLab, memoria bajo aprobación, una skill mínima derivada de un procedimiento real y QA de aislamiento.
