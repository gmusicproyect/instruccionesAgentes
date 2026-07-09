# Instrucciones Cursor — Sistema de Identidad y Método del Ejecutor

Repositorio oficial del protocolo de trabajo para **Cursor Agent Mode** en los proyectos de JP.

La metodología vive en estos archivos, **no en un modelo específico**. El arquitecto es un rol, no una IA concreta. El objetivo es que cualquier ejecutor (Cursor hoy, otro agente mañana) trabaje con el mismo estándar de análisis, ejecución, verificación y reporte.

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
│   ├── 03-instruccion-de-activacion.md
│   └── 04-prompt-auditor-gpt.md
│
├── tests/
│   ├── 05-prueba-de-contrato.md
│   └── 06-eval-calibracion-cursor.md
│
└── references/
    └── bibliografia-protocolo.md
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

# Instalación en un proyecto nuevo

1. Abre un proyecto en Cursor.

2. Copia el contenido de:

```text
prompts/03-instruccion-de-activacion.md
```

3. Pégalo en Cursor Agent Mode.

4. Cursor debe:

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

---

# Alcance de este repositorio

Este repo cubre **identidad** (`rules/01`) y **proceso** (`rules/02`).
La tercera pieza de la trilogía canónica, `loop.mdc` (el motor del ciclo),
vive en el repositorio del proyecto anfitrión (`.agents/cursor-rules/` en
Gmusic). Un proyecto nuevo sin `loop.mdc` propio opera solo con identidad
y proceso hasta que se le instale un motor.

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
2. Abrir Cursor.
3. Pegar el contenido de:

```text
prompts/03-instruccion-de-activacion.md
```

La activación es correcta únicamente si Cursor:

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
| **Proyecto nuevo** | Parte desde `instruccionescursor` (este repo) vía `prompts/03`. |
| **Proyecto activo** | Puede tener reglas más nuevas en su propio `.agents/cursor-rules/` o `.cursor/rules/` — evolucionadas localmente (ver `references/bibliografia-protocolo.md`, sección 6-bis del `02` como ejemplo real). |
| **Propagación** | Cuando una mejora local se prueba y funciona, JP decide si vuelve a `instruccionescursor` para que el próximo proyecto parta ya actualizado. No es automático. |
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

Este repositorio constituye la fuente de verdad para la metodología de trabajo de Cursor en los proyectos de JP.
