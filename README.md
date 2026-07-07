# Instrucciones Cursor — Identidad y método del ejecutor

Sistema de trabajo para Cursor Agent Mode en los proyectos de JP
(Gmusic Academy, Selah Music y futuros). Origen: transferencia de la
metodología del arquitecto (Claude) al ejecutor, diseñada y validada
el 6 de julio de 2026 con un piloto real de punta a punta.

**La idea central:** la metodología vive en estos archivos, no en ningún
modelo. El arquitecto es un rol, no un modelo. El estándar no depende de
qué agentes estén presentes en la sesión.

---

## Cómo se usa (JP)

Al iniciar un proyecto o sesión nueva con Cursor, pégale el bloque de
**`03-instruccion-de-activacion.md`**. Eso es todo. Cursor lee este
repositorio, asume la identidad, copia las reglas a `.cursor/rules/`
del proyecto, y confirma con citas reales antes de ejecutar nada.

## Los archivos, en orden

| Archivo | Qué es | Quién lo usa |
|---|---|---|
| `01-identidad-como-trabaja-claude.md` | CÓMO pensar: leer código real, hipótesis antes de archivos, incómodo primero, plantilla de 5 puntos, señales de alto, rol permanente | Cursor (regla permanente) |
| `02-protocolo-criterio-fable.md` | QUÉ proceso: spec de 4 secciones, mini-brief, niveles de esfuerzo, gates G1–G7, estado persistente, auditoría, decisiones vigentes del arquitecto | Cursor (regla permanente) |
| `03-instruccion-de-activacion.md` | El bloque que JP pega para activar todo en un proyecto nuevo + cómo verificar la activación | JP |
| `04-prompt-auditor-gpt.md` | Prompt reutilizable del auditor (tercer agente), con reglas de veredicto binario | JP → agente GPT |
| `05-prueba-de-contrato.md` | Prueba de presión para validar que un ejecutor absorbió la identidad, con criterios de aprobación y fallo | JP |

## Los tres roles

| Rol | Quién | Responsabilidad |
|---|---|---|
| Arquitecto | Claude (cualquier modelo) o JP | Spec, criterios de aceptación, validación de cierre |
| Ejecutor | Cursor Agent Mode | Implementar bajo el contrato de estos archivos |
| Auditor | Agente GPT | Veredicto binario en tickets Medio-sensible y Alto |

**Autoridad final: JP.** Nada irreversible (push, SQL de producción,
migraciones, borrados) sin su OK explícito. Sin excepciones, sin prisa
que valga.

## Estado de validación

- ✅ Trilogía desplegada en Gmusic Academy (`.agents/cursor-rules/` + sync)
- ✅ Prueba de contrato superada (6 jul 2026)
- ✅ Piloto de transferencia T-LOGIN-REDIRECT: ticket Medio completo con
  mini-brief autónomo, plantilla de 5 puntos, auditoría APRUEBA, commit
  atómico y cero intervención de JP mid-flight

---

*Mantenido por JP. Los agentes proponen cambios a estos archivos;
solo JP los commitea.*
