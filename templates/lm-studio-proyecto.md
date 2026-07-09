# Bloque de proyecto — LM Studio (pegar debajo del System Prompt Fable)

> JP: copia, rellena los campos entre `[...]` y pégalo **debajo** del
> system prompt Fable en el mismo chat / preset.
>
> Un preset = Fable genérico + este bloque. Así el modelo sabe *cómo*
> trabajar (Fable) y *en qué* proyecto está.

---

## Plantilla (copiar y rellenar)

```markdown
# PROYECTO ACTIVO

**Nombre:** [ej. Gmusic Academy]
**Ruta local:** [raíz del repo]/Página de cursos de música
**Stack:** [ej. Vite + React + Express + Prisma]
**Repo / rama:** [ej. gmusicproyect/proyectogmusic · main]

## Comandos de verificación (no inventar)

- TEST: [ej. npm run test] o NO DEFINIDO
- BUILD: [ej. npm run build] o NO DEFINIDO
- VERIFY: [ej. npm run verify] o NO DEFINIDO

## Archivos de estado (si existen)

- Estado: `.agents/PROJECT_STATUS.md`
- Decisiones: `.agents/DECISIONS.md`
- Reglas Cursor (si el proyecto las tiene): `.agents/cursor-rules/`

## Qué SÍ puedes tocar en este chat

- [ej. UI de admin, docs/operations, scripts/ops]

## Qué NO tocar sin OK explícito de JP

- [ej. auth, pagos, schema Prisma, routing global, secrets, Track B]

## Contexto corto (5–10 líneas máx.)

[Qué está vivo en prod, qué ticket importa ahora, qué NO reabrir]

## Modo de este chat

- [ ] Solo asesoría (planes, diffs, sin fingir edición)
- [ ] Ejecución guiada (JP pega archivos / corre comandos)
- [ ] Con tools/MCP (leer/editar disco si están disponibles)

Al inicio de cada sesión: resume en 3 viñetas lo que entiendes del
proyecto y pregunta A/B cuál es el ticket de hoy.
```

---

## Ejemplo rellenado — Gmusic (Track A)

```markdown
# PROYECTO ACTIVO

**Nombre:** Gmusic Academy (Track A)
**Ruta local:** [raíz del repo]/Página de cursos de música
**Stack:** Vite + React + Express + Prisma · Vercel + Render + Supabase
**Repo / rama:** gmusicproyect/proyectogmusic · main

## Comandos de verificación (no inventar)

- TEST: npm run test
- BUILD: npm run build
- VERIFY: npm run verify

## Archivos de estado (si existen)

- Estado: `.agents/PROJECT_STATUS.md`
- Decisiones: `.agents/DECISIONS.md`
- Reglas: `.agents/cursor-rules/` (01, 02, loop.mdc)

## Qué SÍ puedes tocar en este chat

- Docs, specs, briefs para Opus/Cursor
- Análisis de admin / pedagogía / UX
- Scripts ops solo si JP autoriza

## Qué NO tocar sin OK explícito de JP

- Auth, pagos, schema Prisma, routing URL global
- R-001 / R-002, Track B (Next/Sanity)
- Commit / push / apply prod / secrets
- Mezclar tickets (admin password + producto en el mismo diff)

## Contexto corto

- Track A live: landing, funnel demo, zona alumno, admin R-008.
- T-PUB-02: B3 «La menor» con microejercicios en prod (smoke OK).
- Admin actual = bloques de 5 etapas; JP quiere evolucionar a composer
  tipo Simple Guitar (tarjeta → habilidad → puntos video/juego) — eso
  es spec Opus, no improvisar schema.
- Visual D Canva: SUPERSEDED. No reabrir.

## Modo de este chat

- [x] Solo asesoría (planes, diffs, sin fingir edición)
- [ ] Ejecución guiada
- [ ] Con tools/MCP

Al inicio: 3 viñetas de contexto + pregunta A/B del ticket de hoy.
```

---

## Ejemplo mínimo — proyecto nuevo

```markdown
# PROYECTO ACTIVO

**Nombre:** [nombre]
**Ruta local:** [ruta]
**Stack:** [stack]
**Repo / rama:** [repo · rama]

## Comandos

- TEST: NO DEFINIDO
- BUILD: NO DEFINIDO
- VERIFY: NO DEFINIDO

## Qué SÍ / NO

- SÍ: explorar, proponer spec, diffs pequeños
- NO: commit, push, prod, secrets sin OK de JP

## Contexto

[1 párrafo]

## Modo

- [x] Solo asesoría
```
