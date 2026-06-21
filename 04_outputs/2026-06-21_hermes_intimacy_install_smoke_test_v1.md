# Hermes Intimacy: instalación y smoke test local

Fecha: 2026-06-21

## Resumen para Raúl

Hermes quedó instalado en el VPS como usuario `skilland`, en modo CLI local per-user. No quedó instalado dentro del repo: el binario vive en `/home/skilland/.local/bin/hermes`, el código oficial en `/home/skilland/.hermes/hermes-agent` y el estado/config en `/home/skilland/.hermes`.

Versión verificada:

```text
Hermes Agent v0.17.0 (2026.6.19) · upstream 8a506ed3
```

## Qué funcionó

- `hermes version`, `hermes status` y `hermes doctor` corren en el VPS.
- OpenAI Codex quedó configurado como provider con modelo `gpt-5.4`.
- El perfil local `homelab` existe, tiene 0 skills bundled y gateway detenido.
- `homelab` tiene `terminal.cwd` apuntando al repo HomeLab.
- `homelab` tiene `approvals.mode=manual`, `memory.write_approval=true` y `skills.write_approval=true`.
- El smoke test local funcionó: Hermes leyó `AGENTS.md` y `README.md`, respondió en español, identificó la spec 002 y propuso `git status --short --branch`.

## Qué falló o quedó con warning

- El primer OAuth intentó Nous Portal por default; se canceló y se cambió a OpenAI Codex, que era la intención real.
- El perfil `homelab` no heredó auth al crearse limpio; se resolvió reutilizando el auth store Hermes de OpenAI Codex dentro del perfil sin imprimir secretos.
- `hermes doctor` avisa que el config de `homelab` está en versión v0 y puede migrarse a v30.
- Browser tools quedan fuera porque se usó `--skip-browser`; Playwright Chromium no está instalado.
- No hay API keys para herramientas externas; esperado en este microhito.

## Aprendizaje operativo

Hermes ya puede operar como runtime local mínimo dentro del VPS. La separación por perfiles es real: `homelab` tiene su propio home, config, auth, skills, sesiones y memoria. Crear un perfil limpio con `--no-skills` evita heredar skills, pero también obliga a pensar cómo llevar auth y configuración básica al perfil.

## Listo para microhito 003

Sí, con cautela. La base mínima está lista para una prueba de perfil/memoria/skill local. No está listo para gateway, Telegram, webhooks, MCPs externos ni cron.

## Riesgos antes de activar más capas

- Backend local no aísla filesystem.
- Auth OpenAI Codex es un secreto persistente por perfil.
- OAuth de OpenAI Codex puede tener límites de uso.
- Skills y memoria deben seguir con aprobación.
- Migrar config de `homelab` conviene antes de operación más larga.

## Siguiente recomendación

Crear `003_hermes_profile_memory_skill_lab`: ajustar `SOUL.md` de `homelab`, probar memoria con aprobación, crear una skill mínima a partir de un procedimiento real y verificar que no toca sistemas externos.
