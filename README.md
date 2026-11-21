# Platanus Hack 26 — AI Security

> **Estado:** etapa de research. Todavía no hay idea definida; estamos leyendo y juntando notas en `research/`.

## Notas de Jaime: mapa de ideas (dificultad vs impacto)

> Opinión personal de Jaime para discutir, **no una decisión del equipo**. La idea la elegimos entre todos.

![Notas de Jaime: mapa de dificultad vs impacto](research/notas/jaime-aza/mapa-ideas-equipo.svg)

Versión 6.1: la «red de seguridad para agentes de código» en versión acotada queda primera (76), seguida del chequeo previo (75,5), una combinación mínima (73,5) y el swarm de Mauricio acotado (72); incluye las ideas de Federico y Mauricio y una investigación sobre ransomware con IA, y baja el juez por ejecución tras revisarlo a fondo. El círculo blanco es una idea a la que llegamos varios por separado; el anillo rojo punteado marca lo que ya existe o el jurado ya vio en el tour. Razones de cada punto en [mapa-ideas-equipo.md](research/notas/jaime-aza/mapa-ideas-equipo.md), puntaje de las 37 propuestas con la rúbrica en [ranking-propuestas.md](research/notas/jaime-aza/ranking-propuestas.md) y resumen de la investigación en [investigacion-3-problemas-mundiales.md](research/notas/jaime-aza/investigacion-3-problemas-mundiales.md) , [investigacion-4-ransomware-con-ia.md](research/notas/jaime-aza/investigacion-4-ransomware-con-ia.md) e [investigacion-5-slm-vs-frontera.md](research/notas/jaime-aza/investigacion-5-slm-vs-frontera.md).

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
