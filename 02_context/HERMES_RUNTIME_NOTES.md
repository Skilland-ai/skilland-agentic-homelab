# Hermes runtime notes

Fecha: 2026-06-21

## Estado real de instalación

- Estado: instalado en el VPS como usuario `skilland`.
- Método: instalador oficial descargado desde `https://hermes-agent.nousresearch.com/install.sh`.
- Modo: CLI local per-user.
- Binario: `/home/skilland/.local/bin/hermes`.
- Código Hermes: `/home/skilland/.hermes/hermes-agent`.
- Home Hermes default: `/home/skilland/.hermes`.
- Perfil HomeLab: `/home/skilland/.hermes/profiles/homelab`.

## Versión

Salida sanitizada:

```text
Hermes Agent v0.17.0 (2026.6.19) · upstream 8a506ed3
Project: /home/skilland/.hermes/hermes-agent
Python: 3.11.15
OpenAI SDK: 2.24.0
Up to date
```

## Preflight VPS

Salida sanitizada:

```text
pwd: /home/skilland/workspaces/skilland-agentic-homelab
whoami: skilland
hostname: ubuntu
hermes before install: not found
HERMES_HOME before install: missing
git: 2.43.0
curl: 8.5.0
xz: 5.4.5
node: v24.16.0
npm: 11.17.0
python3: 3.12.3
pipx: 1.4.3
docker: 29.5.3
```

## Instalador

- Se ejecutó como `skilland`: `bash 05_scratch/hermes_install/install.sh --skip-browser`.
- No se ejecutó `sudo` manualmente desde la sesión.
- Nota de riesgo: el instalador oficial instaló `ffmpeg` y dependencias del sistema automáticamente durante la ejecución. Queda documentado como side effect del instalador, no como trabajo diario root.
- El instalador creó `~/.hermes/.env`, `~/.hermes/config.yaml`, `~/.hermes/SOUL.md` y sincronizó skills bundled en el perfil default.
- Playwright/Chromium quedó omitido por `--skip-browser`; las herramientas browser quedan ocultas/no disponibles hasta instalación explícita posterior.

## Autenticación

- Provider configurado: OpenAI Codex.
- Modelo default: `gpt-5.4`.
- Auth default: `OpenAI Codex` logged in en `/home/skilland/.hermes/auth.json`.
- Auth `homelab`: `OpenAI Codex` logged in en `/home/skilland/.hermes/profiles/homelab/auth.json`.
- No se registraron claves, tokens, device codes ni secretos en el repo.
- Decisión: Raúl configuró OpenAI Codex manualmente desde su SSH; después se reutilizó el auth store Hermes ya válido dentro del perfil `homelab` sin imprimir su contenido.

## Perfil `homelab`

Salida sanitizada:

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

Configuración aplicada:

```yaml
approvals:
  mode: manual
memory:
  write_approval: true
terminal:
  cwd: /home/skilland/workspaces/skilland-agentic-homelab
skills:
  write_approval: true
model:
  base_url: https://chatgpt.com/backend-api/codex
  provider: openai-codex
  default: gpt-5.4
```

## Doctor

Base default:

- Python, venv, versión, SSL, paquetes requeridos y estructura: OK.
- OpenAI Codex auth: OK.
- Gateway: stopped.
- Canales de mensajería: no configurados.
- Warnings esperados: Nous Portal no logueado, proveedores/API keys extra no configurados, Playwright Chromium no instalado por `--skip-browser`, Skills Hub no inicializado, sin GitHub token.

Perfil `homelab`:

- OpenAI Codex auth: OK.
- Built-in memory active.
- Gateway: stopped.
- Skills: 0.
- Warning: `config.yaml` del perfil aparece como config version v0 -> v30 pendiente de migrar. No bloqueó el smoke test.
- Warning: sin API keys de herramientas externas en `.env`; esperado porque este microhito no habilita web/browser/tool gateway.

## Smoke test local

Comando:

```bash
hermes --profile homelab chat --toolsets file,terminal -q "Lee AGENTS.md y README.md de este repo sin modificar archivos. Responde en español con 5 bullets: qué es el repo, qué no debes hacer, cuál es la spec activa, qué sistemas externos están fuera de alcance y qué comando usarías para ver el estado git."
```

Resultado:

- Ejecutado correctamente.
- Hermes leyó `AGENTS.md` y `README.md`.
- Hermes usó búsqueda/lectura de archivos y terminal.
- Respondió en español con 5 bullets.
- Identificó el repo como Skilland Agentic HomeLab.
- Identificó la spec activa `03_specs/now/002_hermes_intimacy_install_smoke_test.md`.
- Reconoció que no debe conectar canales externos ni tocar sistemas sensibles sin aprobación.
- Propuso `git status --short --branch`.
- No modificó archivos del repo durante el smoke test.

## No alcance verificado

- Gateway no arrancado: no hay proceso `hermes gateway`.
- Telegram no configurado.
- WhatsApp no configurado.
- Gmail/Drive/CRM/Kapso no tocados.
- Slack/Discord no configurados.
- Webhooks no configurados.
- MCPs externos no configurados.
- Cron jobs: 0.
- No se usó `--yolo`.

## Limitaciones y riesgos

- El backend terminal local no es sandbox; Hermes corre con acceso del usuario `skilland`.
- El perfil `homelab` tiene auth OpenAI Codex persistente; conviene tratar `auth.json` como secreto.
- El config del perfil marca migración pendiente; se puede atender en el microhito 003 si se decide.
- Playwright/Chromium no está instalado por decisión de scope; browser tools quedan fuera.
- OAuth/OpenAI Codex puede tener límites de uso externos a Hermes.

## Próxima acción

Planificar `003_hermes_profile_memory_skill_lab`: `SOUL.md` HomeLab mínimo, memoria bajo aprobación, una skill pequeña derivada de un procedimiento real y QA de aislamiento local.
