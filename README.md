# Platanus Hack 26 — AI Security

> **Estado:** etapa de research. Todavía no hay idea definida; estamos leyendo y juntando notas en `research/`.

## Notas de Jaime: mapa de ideas (dificultad vs impacto)

> Opinión personal de Jaime para discutir, **no una decisión del equipo**. La idea la elegimos entre todos.

![Notas de Jaime: mapa de dificultad vs impacto](research/notas/jaime-aza/mapa-ideas-equipo.svg)

Versión 5.3: el chequeo previo de contención pasa a 79,5 con una prueba de separación entre corridas; suma la propuesta unificada de Mauricio, «reversibilidad para agentes» y las ideas de Federico y Mauricio y una investigación sobre ransomware con IA, y baja el juez por ejecución tras revisarlo a fondo. El círculo blanco es una idea a la que llegamos varios por separado; el anillo rojo punteado marca lo que ya existe o el jurado ya vio en el tour. Razones de cada punto en [mapa-ideas-equipo.md](research/notas/jaime-aza/mapa-ideas-equipo.md), puntaje de las 35 propuestas con la rúbrica en [ranking-propuestas.md](research/notas/jaime-aza/ranking-propuestas.md) y resumen de la investigación en [investigacion-3-problemas-mundiales.md](research/notas/jaime-aza/investigacion-3-problemas-mundiales.md) e [investigacion-4-ransomware-con-ia.md](research/notas/jaime-aza/investigacion-4-ransomware-con-ia.md).

## Estructura

| Carpeta | Para qué |
|---|---|
| `research/papers/` | Papers, posts y referencias (PDFs o links) |
| `research/notas/` | Resúmenes, ideas candidatas y preguntas abiertas |
| `src/ph26/ataques/` | Red team: generadores de prompts adversarios, inyecciones, jailbreaks |
| `src/ph26/defensas/` | Blue team: guardrails, filtros, detectores, sandboxing |
| `src/ph26/evals/` | Harness de evaluación: corre ataques contra defensas y mide |
| `datos/crudos/`, `datos/procesados/` | Datasets (no se versionan) |
| `experimentos/` | Una carpeta por corrida, con config y resultados |
| `notebooks/` | Exploración |
| `demo/` | Lo que se muestra al jurado (app/CLI/video) |
| `docs/` | Modelo de amenazas, arquitectura, pitch |
| `entrega/` | Material final para subir |
| `scripts/` | Utilidades sueltas |
| `tests/` | Tests |

## Uso

```bash
cp .env.example .env   # completar claves
make setup
make test
```

## Reglas de la casa

- Los ataques se prueban **solo** contra sistemas propios o con autorización explícita.
- Nada de claves en el repo: van en `.env`.
