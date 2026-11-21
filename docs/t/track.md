AI Security

Construye herramientas concretas que hagan que los modelos más avanzados de IA sean más seguros: atácalos para encontrar sus fallas, defiéndelos o mide con rigor qué tan peligrosos pueden ser.
La prueba

El proyecto tiene que atacar, defender o medir un modelo o agente de IA, o usar IA para que el defensor gane. Si la IA es solo el tema de la app, no es de este track.
Cinco líneas de trabajo

    AI control. Herramientas que aumenten la visibilidad, el control y la seguridad al correr agentes potencialmente desalineados. Si un modelo está intentando causar daño, ¿cómo lo detectas o lo limitas? Ver: The Case for AI Control · ControlArena
    Guardrails y robustez adversarial. Técnicas o herramientas que hagan a los modelos más robustos frente a la presión humana (jailbreaks, inyecciones). Vale la defensa, por ejemplo mejores clasificadores, o la ofensa: encontrar o evaluar nuevos tipos de ataque.
    Cyber evals. Evaluaciones que midan con rigor el uplift que un modelo le da a un humano en tareas de alto riesgo, como la seguridad ofensiva. Ver: Evals Playbook · Inspect Cyber · Cybench
    Interpretabilidad pragmática. Usar las herramientas que hoy permiten leer qué pasa dentro de un modelo (circuit tracing, activation NLAs) para resolver problemas reales de seguridad. Ver: A Pragmatic Vision for Interpretability
    Defensa (def/acc). Herramientas con las que la IA fortalezca más al defensor que al atacante: descubrir y parchar vulnerabilidades de forma autónoma, endurecer sistemas críticos o detectar ataques asistidos por IA (phishing, deepfakes, operaciones de influencia). Ver: d/acc · los 7 cyber reasoning systems finalistas del AIxCC de DARPA (open source)

Califica

    Un monitor que vigila a un agente en un entorno tipo ControlArena y lo frena cuando intenta sabotear su tarea.
    Un clasificador de jailbreaks o inyecciones de prompt, medido contra ataques reales.
    Un generador automático de ataques que encuentra fallas nuevas en un modelo.
    Una eval reproducible que mide cuánto ayuda un modelo a resolver retos de seguridad ofensiva.
    Una sonda sobre las activaciones de un modelo que detecta engaño o intención dañina.
    Un sistema que encuentra y parcha vulnerabilidades solo, o que detecta phishing o deepfakes generados con IA.

No califica

    Agregarle login o cifrado a una app de otro tema.
    Un chatbot que responde preguntas sobre seguridad.
    Ciberseguridad tradicional donde la IA no ataca, no defiende ni es el blanco.
    Un wrapper que solo llama a la API de moderación de un proveedor.
    Un benchmark de capacidades generales sin relación con riesgo.

Preguntas para partir

    Si el agente que corre en tu máquina quisiera hacer daño, ¿cómo te darías cuenta?
    ¿Qué ataque a un modelo funciona hoy y nadie ha medido bien?
    ¿Qué puedes leer dentro de un modelo que no se ve en su respuesta?
    ¿Qué trabajo de un equipo de seguridad podría hacer un agente esta noche?

Frontera

La seguridad de la IA tiene que ser el producto, no una característica. Una demo fuerte muestra un resultado medible: el ataque funcionando y la defensa deteniéndolo, o una eval con números que antes no existían.
