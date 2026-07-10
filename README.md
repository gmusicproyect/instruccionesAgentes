# Instrucciones Agentes — Sistema de Identidad y Método del Ejecutor

Repositorio oficial del protocolo de trabajo para **Agent Mode** en los proyectos de JP.

La metodología vive en estos archivos, **no en un modelo específico**. El arquitecto es un rol, no una IA concreta. El objetivo es que cualquier ejecutor (Cursor, Codex, Claude Code u otro agente) trabaje con el mismo estándar de análisis, ejecución, verificación y reporte.

> **Nombre anterior:** este repositorio se llamaba `instruccionescursor`.
> La URL `https://github.com/gmusicproyect/instruccionescursor` **redirige
> (301)** a `instruccionesAgentes` — es el **mismo** repo (mismo id), no
> una bifurcación. Fuente de verdad única: **`instruccionesAgentes`**.
> Carpetas locales antiguas llamadas `instruccionescursor` (layout plano)
> no son el remoto; no las uses como canónicas.

---

# Objetivo

Este repositorio define:

* Cómo debe pensar el ejecutor antes de modificar código.
* Cómo debe ejecutar un ticket.
* Qué verificaciones son obligatorias.
* Qué acciones requieren autorización humana.
* Cómo activar este comportamiento en cualquier proyecto nuevo.

El objetivo no es producir código más rápido.

El objetivo es producir **cambios verificables, auditables y seguros**.

---

# Estructura del repositorio

```text
.
├── README.md
│
├── rules/
│   ├── 01-identidad-del-ejecutor.md
│   └── 02-protocolo-criterio-fable.md
│
├── prompts/
│   ├── 00-fable-nucleo.md             ← Fable Núcleo v1.2 (cualquier tema)
│   ├── 03-instruccion-de-activacion.md
│   ├── 04-prompt-auditor-gpt.md
│   ├── 05-lm-studio-system-prompt.md  ← capa código / LM Studio
│   └── 06-estrategia-habitos.md       ← capa estrategia + hábitos
│
├── docs/
│   └── diagrams/
│       └── FABLE-NUCLEO-diagrama-flujo.jpg
│
├── tests/
│   ├── 05-prueba-de-contrato.md
│   └── 06-eval-calibracion-cursor.md
│
├── references/
│   └── bibliografia-protocolo.md
│
└── templates/
    ├── loop-template.mdc
    └── lm-studio-proyecto.md          ← bloque por proyecto (LM Studio)
```

---

# Qué contiene cada carpeta

## rules/

Reglas permanentes que definen la identidad y el método del ejecutor.

### 01-identidad-del-ejecutor.md

Define la forma de pensar del ejecutor (Cursor, Codex, o cualquier
agente futuro — el nombre es histórico: se extrajo observando el
método de Claude como arquitecto, pero no es exclusivo de Claude):

* leer código antes de editar
* formular hipótesis
* cambio mínimo
* plantilla de reporte
* comunicación
* señales de alto

---

### 02-protocolo-criterio-fable.md

Define el proceso completo:

* Spec First
* Mini Brief
* niveles de esfuerzo
* Gates G1–G7
* verificación
* PROJECT_STATUS
* auditoría

---

## prompts/

Documentos reutilizables para iniciar sesiones.

### 03-instruccion-de-activacion.md

Prompt que JP pega al comenzar un proyecto nuevo, en CUALQUIER ejecutor
(Cursor, Codex, Claude Code u otro). Incluye la tabla de dónde instala
cada herramienta sus reglas permanentes.

Hace que el ejecutor:

* lea este repositorio
* adopte la identidad
* copie las reglas a `.cursor/rules/`
* confirme con citas reales antes de comenzar

---

### 04-prompt-auditor-gpt.md

Prompt reutilizable para un agente GPT en rol de auditor técnico.

---

### 00-fable-nucleo.md

**Fable Núcleo v1.2** — motor de decisión para cualquier tema.
Incluye continuidad conversacional (Modo A decisión / Modo B entrega /
Modo C trivial). Pegar solo o debajo de una capa de dominio.

### 05-lm-studio-system-prompt.md

Capa **código** (Fable genérico v3.1) para LM Studio / modelos locales.
**Sin nombre de producto:** asesor sin tools, G1–G7, modos ASESOR /
AUDITOR / TOOLS. El contexto de un proyecto concreto va en
`templates/lm-studio-proyecto.md` (plantilla vacía), pegado debajo.
Preset recomendado: Núcleo + esta capa + bloque de proyecto.

### 06-estrategia-habitos.md

Capa de dominio (principios tipo Atomic Habits + Art of War).
Usar con Núcleo encima; no sustituye al Núcleo.

---

## tests/

Pruebas para comprobar que el ejecutor realmente absorbió la metodología.

> ⚠️ **Carpeta exclusiva de JP.** El ejecutor NO debe leer estos archivos:
> contienen las trampas verbatim, y un ejecutor que las leyó ya no puede
> ser evaluado limpiamente con ellas. La instrucción de activación excluye
> esta carpeta de forma explícita.

### 05-prueba-de-contrato.md

Prueba bajo presión.

Valida que el ejecutor:

* no salte gates
* no haga push
* no comente tests
* no improvise

---

### 06-eval-calibracion-cursor.md

Evalúa calibración.

Detecta:

* under-effort
* over-effort
* esfuerzo correctamente proporcionado

---

## references/

Documentación de respaldo.

### bibliografia-protocolo.md

Explica el fundamento metodológico del sistema y relaciona cada regla con sus obras de referencia.

---

## templates/

### loop-template.mdc

El **motor del ciclo** en versión genérica: la regla ejecutable
(ESTADO → RUTINA → VERIFICACIÓN → CRITERIO DE SALIDA) que convierte la
prosa de `01`+`02` en un ciclo mecánico que corre en cada sesión.

Se instala copiándolo a `.cursor/rules/loop.mdc` (en Cursor) o integrándolo
en `AGENTS.md` / `CLAUDE.md`, y reemplazando los placeholders
`{{TEST_CMD}}`, `{{BUILD_CMD}}`, `{{VERIFY_CMD}}` con los comandos
reales del proyecto.

### lm-studio-proyecto.md

Bloque corto por proyecto para pegar **debajo** del system prompt Fable
en LM Studio. Define stack, comandos de verify, qué sí/no tocar y modo
del chat (asesoría vs tools).

---

# Instalación en un proyecto nuevo

## A) Cursor / Codex / Claude Code (con acceso a repo)

1. Abre un proyecto en tu IDE con agente (Cursor, Codex, Claude Code, etc.).

2. Copia el contenido de:

```text
prompts/03-instruccion-de-activacion.md
```

3. Pégalo en el chat del ejecutor (Agent Mode o equivalente).

4. El ejecutor debe:

* leer las reglas de:

```text
rules/01-identidad-del-ejecutor.md
rules/02-protocolo-criterio-fable.md
```

* copiar esos archivos a:

```text
.cursor/rules/
```

* confirmar con citas reales antes de ejecutar cualquier tarea.

Si responde únicamente "Entendido" o no cita reglas concretas, la activación no fue correcta.

## B) LM Studio (modelo local, sin GitHub automático)

Presets sugeridos:

* `Fable — Núcleo` → solo `prompts/00-fable-nucleo.md`
* `Fable — Código` → Núcleo + `05-lm-studio-system-prompt.md` +
  bloque rellenado de `templates/lm-studio-proyecto.md`
* `Fable — Estrategia y Hábitos` → Núcleo + `06-estrategia-habitos.md`

1. Abre el prompt del preset y copia desde `INICIO SYSTEM PROMPT` hasta
   `FIN SYSTEM PROMPT` (si el archivo lo tiene; Núcleo y capas lo usan).

2. En LM Studio → Chat → System Prompt: pega ese bloque.

3. (Opcional, capa código) Debajo, pega un bloque de proyecto rellenado
   desde `templates/lm-studio-proyecto.md`.

4. Params sugeridos Núcleo: reasoning high · temperature 0.4–0.6 ·
   context ≥ 8k.

5. Pruebas: pie de `00-fable-nucleo.md` (incl. Prueba 6 continuidad) y
   pie de `05` si usas capa código.

---

# Alcance de este repositorio

Este repo cubre la trilogía completa: **identidad** (`rules/01`),
**proceso** (`rules/02`) y **motor** (`templates/loop-template.mdc`,
versión genérica con placeholders). Cada proyecto instala el template
del loop con sus propios comandos de verificación; la versión
especializada de Gmusic vive en su repo (`.agents/cursor-rules/loop.mdc`).
Un proyecto puede operar solo con `01`+`02` si aún no define comandos
de verificación, pero el ciclo completo requiere las tres piezas.

---

# Roles del sistema

| Rol        | Responsabilidad                                       |
| ---------- | ----------------------------------------------------- |
| Arquitecto | Diseña la solución, define la spec y valida el cierre |
| Ejecutor   | Implementa el cambio siguiendo este protocolo         |
| Auditor    | Revisa el diff contra la spec y los gates             |
| JP         | Autoriza toda acción irreversible                     |

---

# Reglas inquebrantables

Nunca realizar sin autorización explícita de JP:

* Push
* Merge
* SQL de producción
* Migraciones
* Cambios destructivos
* Seeds en producción
* Eliminación de datos
* Credenciales o secrets en código

---

# Smoke test del repositorio

Después de cualquier cambio estructural:

1. Abrir un proyecto vacío.
2. Abrir el ejecutor (Cursor, Codex, Claude Code u otro).
3. Pegar el contenido de:

```text
prompts/03-instruccion-de-activacion.md
```

La activación es correcta únicamente si el ejecutor:

* encuentra los archivos en sus rutas actuales;
* cita reglas reales de `rules/01-identidad-del-ejecutor.md`;
* cita reglas reales de `rules/02-protocolo-criterio-fable.md`;
* no ejecuta ninguna acción antes de la confirmación.

Si alguno de esos puntos falla, existe una referencia rota en el repositorio.

---

# Sincronización del método

Este repo es **plantilla inicial y referencia portable** — no es el canon
en tiempo real de un proyecto activo. Regla de uso:

| Situación | Qué hacer |
|---|---|
| **Proyecto nuevo** | Parte desde `instruccionesAgentes` (este repo) vía `prompts/03`. |
| **Proyecto activo** | Puede tener reglas más nuevas en su propio `.agents/cursor-rules/` o `.cursor/rules/` — evolucionadas localmente (ver `references/bibliografia-protocolo.md`, sección 6-bis del `02` como ejemplo real). |
| **Propagación** | Cuando una mejora local se prueba y funciona, JP decide si vuelve a `instruccionesAgentes` para que el próximo proyecto parta ya actualizado. No es automático. |
| **Riesgo si no se sincroniza** | Un proyecto nuevo que instala solo desde este repo puede recibir una versión **stale** si un proyecto anterior avanzó las reglas y esa mejora nunca volvió aquí. |

---

# Licencia y aportes

Este repositorio se distribuye bajo licencia **MIT** (ver `LICENSE`).
Cualquiera puede usar, copiar o adaptar este contenido dando crédito al
autor original.

**Aportes de terceros:** se reciben vía Pull Request. Ningún cambio entra
a `main` sin revisión y aprobación de JP — la licencia da permiso de
reuso, no acceso de escritura directa al repositorio oficial.

---

# Estado

* ✅ Identidad del ejecutor
* ✅ Protocolo de ejecución
* ✅ Activación
* ✅ Auditor
* ✅ Pruebas de contrato
* ✅ Evaluación de calibración
* ✅ Bibliografía

Este repositorio constituye la fuente de verdad para la metodología de trabajo de los agentes ejecutores en los proyectos de JP.
