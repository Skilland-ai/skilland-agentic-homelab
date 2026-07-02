# Hermes identity memory foundation v1

Fecha: 2026-06-21

## Resumen para Raúl

El perfil Hermes `homelab` ya no arranca como asistente genérico. Ahora tiene una identidad base como Hermes HomeLab, una memoria operativa mínima y un perfil de usuario centrado en cómo trabajas tú dentro del laboratorio.

Esta no es la identidad perfecta ni definitiva. Es una primera fundación corta, testeable y alineada con la North Star para que las siguientes sesiones de Hermes partan del sitio correcto.

## Por qué tocaba esto ahora

Antes de skills, cron, Gateway, browser, Telegram, WhatsApp, Gmail, Drive, CRM, MCPs o mission control, Hermes necesita saber quién es y qué papel ocupa.

Sin `SOUL.md`, `MEMORY.md` y `USER.md` bien sembrados, cualquier automatización posterior partiría de un agente técnicamente capaz pero conceptualmente genérico. Eso es frágil: puede leer contexto, pero no tiene criterio propio estable.

El orden correcto para HomeLab es:

1. Identidad y límites.
2. Memoria pequeña y curada.
3. Pruebas locales.
4. Repos reales read-only.
5. Solo después, skills, loops, canales o integraciones.

## Qué quedó en `SOUL.md`

`SOUL.md` define a Hermes como Hermes HomeLab: operador principal del Skilland Agentic HomeLab.

Incluye:

- North Star como brújula estratégica.
- HomeLab como bajada experimental al VPS real.
- Hermes como núcleo operativo que estamos aprendiendo a dominar.
- Codex como operador técnico residente, arquitecto y evaluador.
- Raúl como director de prioridad, riesgo y criterio final.
- Repos como fábricas de trabajo.
- Microhitos, pruebas pequeñas y documentación como forma de avance.
- Separación entre documentación oficial, comunidad e hipótesis.
- Autonomía alta dentro del laboratorio interno.
- Escalado obligatorio para sistemas externos, producción, secretos, mensajes reales y cambios irreversibles.

No incluye rutas largas, comandos, workflows, specs activas ni documentación completa de Hermes. Eso pertenece al repo, a contexto o a futuras skills.

## Qué quedó en `USER.md`

`USER.md` describe cómo debe entender Hermes a Raúl como operador humano del laboratorio.

Incluye:

- Raúl dirige HomeLab como CEO/CTO funcional de Skilland/Reboot.
- Quiere outputs en español.
- Prefiere claridad directa, pragmatismo y explicaciones en cristiano.
- Quiere ejecución real por microhitos, no teoría larga.
- Tolera rotura interna si se documenta aprendizaje, riesgo y siguiente acción.
- No quiere arquitectura prematura ni sobrecautela inútil.
- Exige autorización clara para acciones externas, clientes, producción, secretos, mensajes reales o cambios irreversibles.

No incluye biografía larga, detalles privados, credenciales ni preferencias irrelevantes.

## Qué quedó en `MEMORY.md`

`MEMORY.md` guarda hechos operativos durables para que Hermes no arranque frío en cada sesión.

Incluye:

- HomeLab corre en el VPS real como usuario `skilland`.
- Los repos viven en `/home/skilland/workspaces`.
- `skilland-agentic-north-star` es el repo estratégico.
- `skilland-agentic-homelab` es el repo operativo.
- North Star gobierna visión; HomeLab ejecuta experimentos.
- Hermes es el núcleo objetivo del HomeLab.
- Codex es operador técnico residente y arquitecto/evaluador.
- Docs oficiales y repo oficial de Hermes tienen prioridad técnica.
- Comunidad/X/YouTube sirven como inspiración, no como verdad oficial.
- No activar canales externos, webhooks, MCPs externos, browser, cron, Gateway o producción sin microhito explícito.

No se metieron dumps largos ni la North Star completa. La memoria queda pequeña a propósito.

## Qué queda fuera

Esta spec no conectó ni configuró:

- Gateway.
- Telegram.
- WhatsApp.
- Gmail.
- Drive.
- CRM.
- Slack.
- Discord.
- Kapso.
- Webhooks.
- MCPs externos.
- Cron jobs.
- Browser/Chrome/Chromium/Playwright.
- Skills.
- Mission control.
- Meta-harness.

Tampoco se tocaron `.env`, `auth.json`, tokens ni secretos.

## Relación estratégica

La cadena que Hermes debe tener clara ahora es:

```text
North Star
  -> fija visión, principios y dirección

HomeLab
  -> prueba esa visión en el VPS real, con libertad interna y documentación

Hermes
  -> núcleo operativo que debe ganar identidad, memoria, loops y criterio

Codex
  -> operador técnico residente, arquitecto/evaluador y ejecutor de microhitos

Raúl
  -> director del laboratorio, prioridad, producto, riesgo y aprobación final
```

Divi-DClick no gobierna HomeLab. Recibirá después aprendizajes más sobrios, seguros y vendibles. La productización viene todavía más tarde, cuando existan patrones repetibles probados.

## Estado verificado

- `SOUL.md`: `2163 B`
- `MEMORY.md`: `1337 B`
- `USER.md`: `956 B`
- `MEMORY.md` queda bajo el límite oficial de `2200` caracteres aproximados.
- `USER.md` queda bajo el límite oficial de `1375` caracteres aproximados.
- `prompt-size` muestra:
  - memory: `1,671 B`
  - user profile: `1,290 B`
  - skills index: `0 B`
- Hermes responde ya como Hermes HomeLab en sesión nueva.
- Hermes distingue `SOUL.md`, `USER.md`, `MEMORY.md` y `AGENTS.md`.
- Hermes rechazó conectar WhatsApp dentro de esta spec.
- Hermes resumió correctamente la cadena North Star -> HomeLab -> Divi-DClick -> productización.
- `Gateway: stopped` según `profile show`.
- `Skills: 0` según `profile show`.
- No hay `SKILL.md` en el perfil.
- Incidencia mitigada: Hermes auto-generó una skill durante QA porque `skills.write_approval` está en `false`; fue eliminada y el estado final vuelve a `Skills: 0`.

## Decisiones tomadas

- Codex ejecutó la cirugía inicial de identidad/memoria.
- Hermes quedó como sujeto de prueba, no como ejecutor principal de su propia configuración.
- Se usó el contenido semilla de la spec sin expandirlo.
- Se documentó el estado real de configuración permisiva (`approvals.mode: false`, `memory.write_approval: false`, `skills.write_approval: false`) sin revertirlo.
- Se mantuvo la memoria como snapshot pequeño, no como wiki.

## Riesgos

- `homelab` corre con permisos reales del usuario `skilland`; el perfil no sandboxea filesystem.
- El perfil tiene auth persistente de OpenAI Codex en `auth.json`, que debe tratarse como secreto.
- `approvals.mode: false` reduce fricción pero aumenta riesgo si se usan prompts agresivos o integraciones.
- `memory.write_approval: false` permite que Hermes escriba memoria sin staging; conviene vigilarlo tras sesiones largas.
- La migración de config `v0 -> v30` sigue pendiente.
- Procesos `tui_gateway.*` pueden confundirse con Gateway de mensajería; `profile show` sigue siendo la señal de estado del Gateway real.

## Siguiente recomendación

Siguiente microhito recomendado:

```text
005_hermes_first_real_repo_readonly_operator
```

Objetivo: elegir un repo real de bajo riesgo, pedir a Hermes una lectura read-only, obtener una síntesis operativa y proponer un primer microhito útil. Sin conectar externos, sin escribir producción y sin crear skills todavía.

Alternativa si Raúl nota fricción de tono tras usar Hermes manualmente:

```text
005_hermes_identity_iteration_after_human_trial
```

Objetivo: probar Hermes como humano, capturar fricciones reales y ajustar `SOUL.md` una sola vez antes de avanzar a loops.
