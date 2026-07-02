# Hermes profile foundation

Fecha: 2026-06-21

## Perfil afectado

- Perfil: `homelab`
- Home del perfil: `/home/skilland/.hermes/profiles/homelab`
- `SOUL.md`: `/home/skilland/.hermes/profiles/homelab/SOUL.md`
- `MEMORY.md`: `/home/skilland/.hermes/profiles/homelab/memories/MEMORY.md`
- `USER.md`: `/home/skilland/.hermes/profiles/homelab/memories/USER.md`
- Cwd esperado: `/home/skilland/workspaces/skilland-agentic-homelab`

## Qué cambió

- `SOUL.md` dejó de ser el default genérico de Hermes.
- `MEMORY.md` y `USER.md` fueron creados en `memories/`.
- `prompt-size` ya muestra memoria y user profile mayores que `0 B`.

## Resumen de `SOUL.md`

Hermes se define como Hermes HomeLab: operador principal del Skilland Agentic HomeLab. Su misión es ayudar a Raúl a convertir el VPS de Skilland/Reboot en un laboratorio agentic rompible, útil y documentado.

La identidad conecta North Star, HomeLab, Hermes, Codex, Raúl y repos como fábricas. El tono esperado es español, directo, técnico, accionable y sin teatro de cortesía.

## Resumen de `USER.md`

Raúl dirige HomeLab como CEO/CTO funcional de Skilland/Reboot. Prefiere español, claridad directa, pragmatismo, explicaciones en cristiano, microhitos y ejecución real antes que teoría larga.

Tolera rotura interna si deja aprendizaje documentado, pero acciones externas, producción, clientes, secretos, mensajes reales o cambios irreversibles requieren autorización clara.

## Resumen de `MEMORY.md`

Hermes recuerda que HomeLab corre en el VPS real como usuario `skilland`, que los repos viven en `/home/skilland/workspaces`, que North Star gobierna visión y HomeLab ejecuta experimentos.

También recuerda que Hermes es el núcleo objetivo del HomeLab, Codex es operador técnico residente, y que docs/repo oficiales de Hermes tienen prioridad sobre comunidad/X/YouTube.

## Límites de esta fundación

- No se activó Gateway.
- No se conectó Telegram, WhatsApp, Gmail, Drive, CRM, Slack, Discord ni Kapso.
- No se configuraron webhooks, MCPs externos, browser, cron jobs ni skills.
- No se tocó `.env`, `auth.json`, tokens ni secretos.
- No se resolvió la migración de config `v0 -> v30`.
- No se diseñó mission control ni meta-harness.
- Incidencia mitigada: Hermes auto-generó una skill durante QA porque `skills.write_approval` está en `false`; se eliminó y el estado final del perfil vuelve a `Skills: 0`.

## Estado operativo relevante

- Hermes v0.17.0.
- Provider/modelo del perfil: `openai-codex` / `gpt-5.4`.
- `Gateway: stopped` según `profile show`.
- `Skills: 0` según `profile show`.
- Config real del perfil al cierre:
  - `approvals.mode: false`
  - `memory.write_approval: false`
  - `skills.write_approval: false`

## Siguiente microhito recomendado

`005_hermes_first_real_repo_readonly_operator`: elegir un repo real de bajo riesgo, pedir a Hermes una lectura read-only, producir una síntesis operativa y proponer el primer microhito útil sin conectar sistemas externos ni escribir producción.

## Actualización 2026-07-02 — v1.1 estratégica

- Se aplicó una iteración estratégica v1.1 de `SOUL.md`, `MEMORY.md` y `USER.md` del perfil `homelab`.
- Orientación: más ambiciosa en visión y más sobria en permisos; Hermes queda formulado como capa operativa residente para convertir North Star en capacidades reales probadas dentro del VPS/repos.
- Mejoras principales: North Star más explícita, producto antes que arquitectura, aprendizaje transferible, repos como fábricas/departamentos, libertad interna con control en cliente, y brainstorming/validación antes de prompts ejecutivos cuando la decisión es estratégica.
- Checks finales: `SOUL.md` `3091 B`, `MEMORY.md` `1814 B`, `USER.md` `1182 B`; `prompt-size` muestra `memory: 2,148 B` y `user profile: 1,518 B`.
- Tests de sesión nueva pasaron: identidad/North Star, decisión estratégica no validada, restricción ante WhatsApp/Gmail y Gateway no arrancado.
- No se activaron sistemas externos, Gateway, canales, cron, browser, MCPs, webhooks ni cambios de config. No se tocaron `.env`, `auth.json`, tokens ni secretos.
