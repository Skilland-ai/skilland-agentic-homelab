# Run 01: Hermes intimacy install + smoke test

Fecha: 2026-06-21

## Objetivo

Instalar/verificar Hermes en el VPS como usuario `skilland`, configurar auth persistente, crear perfil local `homelab`, ejecutar smoke test local sin modificar archivos y cerrar QA contra la spec 002.

## Lecturas previas

- `AGENTS.md`
- `01_harness/RULES.md`
- `01_harness/STACK.md`
- `01_harness/TASKFLOW.md`
- Todos los archivos en `02_context/`
- `03_specs/now/002_hermes_intimacy_install_smoke_test.md`
- `03_runs/2026-06-21_hermes_deep_research_run_01.md`
- `04_outputs/2026-06-21_hermes_metagame_initial_synthesis.md`
- `shared/skills/ship-output/SKILL.md`
- `shared/skills/qa-review/SKILL.md`
- Docs oficiales cacheadas indicadas por la spec.

## Git status inicial

```text
 M 03_specs/decisions.md
 D 03_specs/now/001_hermes_deep_research.md
?? 03_specs/done/
?? 03_specs/now/002_hermes_intimacy_install_smoke_test.md
```

## Preflight

Comandos ejecutados:

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

Salida sanitizada:

```text
pwd: /home/skilland/workspaces/skilland-agentic-homelab
whoami: skilland
hostname: ubuntu
hermes: not found
HERMES_HOME_MISSING
git version 2.43.0
curl 8.5.0
xz 5.4.5
node v24.16.0
npm 11.17.0
python3 3.12.3
pipx 1.4.3
docker 29.5.3
```

Checksum inbox:

```text
96e85ca66044eafe5606d2cb9eebc29ada5568c0b4da88d34cfd7c951f2f8503  00_inbox/hermes_sources.md
```

## Instalación

Comandos ejecutados:

```bash
mkdir -p 05_scratch/hermes_install
curl -fsSL https://hermes-agent.nousresearch.com/install.sh -o 05_scratch/hermes_install/install.sh
sed -n '1,180p' 05_scratch/hermes_install/install.sh
bash 05_scratch/hermes_install/install.sh --skip-browser
export PATH="$HOME/.local/bin:$PATH"
```

Resultado:

- Instalado en `/home/skilland/.hermes/hermes-agent`.
- Launcher instalado en `/home/skilland/.local/bin/hermes`.
- `~/.local/bin` añadido a `/home/skilland/.bashrc`.
- `~/.hermes/.env`, `~/.hermes/config.yaml` y `~/.hermes/SOUL.md` creados.
- Skills bundled sincronizadas en perfil default.
- Browser engine omitido por `--skip-browser`.

Nota:

- El instalador oficial instaló `ffmpeg` y dependencias del sistema automáticamente. No ejecuté `sudo` manualmente, pero queda registrado como side effect del instalador.

## Versión

Comando:

```bash
hermes version
```

Salida:

```text
Hermes Agent v0.17.0 (2026.6.19) · upstream 8a506ed3
Project: /home/skilland/.hermes/hermes-agent
Python: 3.11.15
OpenAI SDK: 2.24.0
Up to date
```

## Autenticación

Secuencia:

- El wizard abrió inicialmente Nous Portal por default; se canceló.
- Raúl ejecutó `hermes model` desde su SSH y eligió OpenAI Codex.
- Hermes importó credenciales existentes de Codex CLI y actualizó `model.provider=openai-codex`.
- Se verificó `OpenAI Codex ✓ logged in` en `hermes status`.
- Para `homelab`, se configuró `model.provider=openai-codex`, `model.default=gpt-5.4`, `model.base_url=https://chatgpt.com/backend-api/codex` y se instaló el auth store válido en `/home/skilland/.hermes/profiles/homelab/auth.json` sin imprimir su contenido.

No se copiaron secretos al repo, run note ni output.

## Doctor base

Comando:

```bash
hermes doctor
```

Resultado sanitizado:

- Seguridad: sin advisories activos.
- Python/venv/versiones: OK.
- Config default: OK.
- OpenAI Codex auth: logged in.
- Gateway: stopped.
- Warnings esperados: Nous Portal no logueado, APIs extra no configuradas, Playwright Chromium omitido por `--skip-browser`, Skills Hub no inicializado, sin GitHub token.

## Perfil `homelab`

Comandos:

```bash
hermes profile list
hermes profile create homelab --no-skills --description "Perfil local de laboratorio para Skilland Agentic HomeLab."
hermes profile show homelab
hermes --profile homelab config set terminal.cwd /home/skilland/workspaces/skilland-agentic-homelab
hermes --profile homelab config set approvals.mode manual
hermes --profile homelab config set memory.write_approval true
hermes --profile homelab config set skills.write_approval true
```

Resultado:

```text
Profile: homelab
Path:    /home/skilland/.hermes/profiles/homelab
Model:   gpt-5.4 (openai-codex)
Gateway: stopped
Skills:  0
.env:    exists
SOUL.md: exists
Alias:   homelab -> hermes -p homelab
```

Config verificada:

```yaml
approvals.mode: manual
memory.write_approval: true
terminal.cwd: /home/skilland/workspaces/skilland-agentic-homelab
skills.write_approval: true
model.provider: openai-codex
model.default: gpt-5.4
```

## Doctor `homelab`

Comando:

```bash
hermes --profile homelab doctor
```

Resultado sanitizado:

- OpenAI Codex auth: logged in.
- Built-in memory active.
- Gateway: stopped.
- Profile found: `homelab: gpt-5.4`.
- Warnings: `.env` sin API key, config version v0 -> v30 pendiente, Playwright Chromium no instalado, APIs externas no configuradas. No bloquea el smoke test local.

## Smoke test

Comando:

```bash
hermes --profile homelab chat --toolsets file,terminal -q "Lee AGENTS.md y README.md de este repo sin modificar archivos. Responde en español con 5 bullets: qué es el repo, qué no debes hacer, cuál es la spec activa, qué sistemas externos están fuera de alcance y qué comando usarías para ver el estado git."
```

Resultado sanitizado:

```text
Hermes leyó AGENTS.md y README.md.
Usó file read, find y terminal.
Respondió en español con 5 bullets.
Identificó Skilland Agentic HomeLab.
Identificó 03_specs/now/002_hermes_intimacy_install_smoke_test.md como spec activa.
Indicó no conectar canales externos ni tocar sistemas sensibles sin aprobación.
Propuso git status --short --branch.
Session: 20260621_154235_c264ca
```

## Verificación de no alcance

Comandos:

```bash
ps -eo pid,args | rg '[h]ermes.*gateway|[g]ateway run|[g]ateway start' || true
hermes profile show homelab
git status --short
sha256sum 00_inbox/hermes_sources.md
```

Resultado:

- No hay proceso gateway.
- `homelab` muestra `Gateway: stopped`.
- Canales externos no configurados.
- Webhooks no configurados.
- MCPs externos no configurados.
- Cron jobs: 0.
- No se usó `--yolo`.
- `00_inbox/hermes_sources.md` conserva checksum `96e85ca66044eafe5606d2cb9eebc29ada5568c0b4da88d34cfd7c951f2f8503`.

## Git status final

```text
 M 03_specs/decisions.md
 D 03_specs/now/001_hermes_deep_research.md
?? 03_specs/done/
?? 03_specs/now/002_hermes_intimacy_install_smoke_test.md
?? 05_scratch/hermes_install/
```

Más los entregables creados por esta spec:

```text
?? 02_context/HERMES_RUNTIME_NOTES.md
?? 03_runs/2026-06-21_hermes_intimacy_install_smoke_test_run_01.md
?? 04_outputs/2026-06-21_hermes_intimacy_install_smoke_test_v1.md
```

## Decisiones tomadas

- Instalar Hermes per-user en el VPS, no dentro del repo.
- Usar OpenAI Codex en lugar de Nous Portal.
- Crear `homelab` con `--no-skills`.
- Mantener backend terminal local por ahora, con `terminal.cwd` limitado al repo.
- No migrar config ni instalar browser tooling en este microhito.

## Bloqueos

No hay bloqueo final. Auth quedó funcional con OpenAI Codex.

## Riesgos

- El instalador instaló dependencias del sistema automáticamente.
- Backend local no es sandbox.
- Auth OpenAI Codex por perfil debe tratarse como secreto.
- Config de `homelab` tiene migración pendiente.
- OpenAI Codex puede imponer límites de uso.

## QA contra criterios de aceptación

| Criterio | Estado | Evidencia |
|---|---|---|
| Existe `02_context/HERMES_RUNTIME_NOTES.md` | pass | Archivo creado |
| Existe `04_outputs/2026-06-21_hermes_intimacy_install_smoke_test_v1.md` | pass | Archivo creado |
| Existe `03_runs/2026-06-21_hermes_intimacy_install_smoke_test_run_01.md` | pass | Este archivo |
| `hermes` instalado o ausencia documentada | pass | `/home/skilland/.local/bin/hermes` |
| `hermes version` registrado | pass | v0.17.0 registrado |
| `hermes doctor` registrado | pass | Default y `homelab` registrados |
| Auth persistente o `blocked: auth` | pass | OpenAI Codex logged in default y `homelab` |
| Existe perfil `homelab` | pass | `hermes profile show homelab` |
| `terminal.cwd` apunta al repo | pass | Config verificada |
| `approvals.mode=manual` | pass | Config verificada |
| `memory.write_approval=true` | pass | Config verificada |
| `skills.write_approval=true` | pass | Config verificada |
| Smoke test ejecutado o bloqueo concreto | pass | Smoke test ejecutado correctamente |
| No root para trabajo diario | pass con nota | Trabajo ejecutado como `skilland`; instalador oficial hizo side effect de paquetes sistema |
| No `sudo` salvo bloqueo | pass con nota | No ejecuté comando `sudo`; instalador manejó dependencias automáticamente |
| No `--yolo` | pass | No usado |
| No Gateway | pass | Sin proceso gateway; status stopped |
| No canales externos | pass | Status muestra canales no configurados |
| No webhooks | pass | No configurados |
| No MCPs externos | pass | No configurados |
| No producción | pass | Solo VPS HomeLab y Hermes local |
| `00_inbox/hermes_sources.md` intacto | pass | Checksum idéntico |
| Git status final sin cambios inesperados fuera de spec/scratch/entregables | pass | Cambios previos + scratch + entregables |
| Siguiente acción clara | pass | Microhito 003 recomendado |

## Siguiente acción recomendada

Crear `003_hermes_profile_memory_skill_lab`: ajustar `SOUL.md` de `homelab`, probar memoria con aprobación, crear una skill mínima y revisar aislamiento antes de cron/gateway/MCP.
