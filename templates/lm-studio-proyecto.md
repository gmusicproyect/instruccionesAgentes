# Bloque de proyecto — LM Studio (plantilla vacía)

> Pegar **debajo** del system prompt Fable genérico
> (`prompts/05-lm-studio-system-prompt.md`).
>
> Un preset = Fable genérico + este bloque rellenado.
> El protocolo (cómo actuar) no cambia; solo cambia este bloque por proyecto.
>
> **No** incluyas rutas con `/Users/nombre/` en copias públicas.

---

## Plantilla (copiar y rellenar)

```markdown
# PROYECTO ACTIVO

**Nombre:** [nombre del proyecto]
**Ruta local:** [raíz del repo — genérica, sin /Users/...]
**Stack:** [lenguajes / frameworks]
**Repo / rama:** [org/repo · rama]

## Comandos de verificación (no inventar)

- TEST: [comando] o NO DEFINIDO
- BUILD: [comando] o NO DEFINIDO
- VERIFY: [comando] o NO DEFINIDO

## Archivos de estado (si existen)

- Estado: `.agents/PROJECT_STATUS.md` (o equivalente)
- Decisiones: `.agents/DECISIONS.md` (o equivalente)
- Reglas del ejecutor: [ruta si aplica]

## Qué SÍ puedes tocar en este chat

- [lista]

## Qué NO tocar sin OK explícito del humano

- [lista: auth, pagos, schema, secrets, prod, etc.]

## Contexto corto (5–10 líneas máx.)

[Qué está vivo, qué ticket importa, qué NO reabrir]

## Modo de este chat

- [ ] Solo asesoría (planes, diffs, sin fingir edición)  ← default
- [ ] Ejecución guiada (humano pega archivos / corre comandos)
- [ ] Con tools/MCP (leer/editar disco si están disponibles)

Al inicio de cada sesión: 3 viñetas de contexto + pregunta A/B del ticket
de hoy. Si no hay ticket, pregunta cuál es (A/B + recomendación).
```

---

## Ejemplo mínimo (placeholders, sin producto concreto)

```markdown
# PROYECTO ACTIVO

**Nombre:** [nombre]
**Ruta local:** [raíz del repo]
**Stack:** [stack]
**Repo / rama:** [org/repo · rama]

## Comandos

- TEST: NO DEFINIDO
- BUILD: NO DEFINIDO
- VERIFY: NO DEFINIDO

## Qué SÍ / NO

- SÍ: explorar, proponer spec, diffs pequeños
- NO: commit, push, prod, secrets sin OK del humano

## Contexto

[1 párrafo]

## Modo

- [x] Solo asesoría
```
