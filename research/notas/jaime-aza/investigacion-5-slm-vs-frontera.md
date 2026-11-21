# Notas de Jaime: ¿modelos pequeños ajustados o modelos de frontera para red teaming y hardening?

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Búsqueda del 21-11-2026 para la propuesta de Mauricio ([m-propuesta_swarm_slm_red_team_hardening.md](../m-propuesta_swarm_slm_red_team_hardening.md)). Varias cifras salen de resúmenes de papers y no de la fuente completa; abrirlas antes de citarlas.

## Respuesta corta

Conviene un esquema **híbrido**, no un swarm solo de modelos pequeños ajustados: modelos de frontera por API para explotar y parchar, y modelos abiertos ya ajustados para el triage local y como respaldo cuando la frontera se niegue. Coincide con lo que Mauricio dejó en su sección 8: los modelos pequeños ganan en subtareas acotadas y verificables, no en razonamiento largo.

## Lo que encontré

- **Ataques de varios pasos: gana la frontera con holgura.** El mejor modelo pequeño publicado ronda 15 a 20 % en Cybench (Cyber-Zero-32B 17,5 %, Pentest-R1 15 %); Claude Sonnet 4.5 llega a 46 %, y los modelos de 2026 puntúan más alto en CyberGym.
- **Abierto no es pequeño.** Los modelos abiertos que compiten con la frontera en ciber (GLM-5.x, DeepSeek V4) tienen cientos de miles de millones de parámetros y no caben en una GPU de 24 GB.
- **Tareas estrechas: ganan los pequeños.** Un modelo de 4 mil millones logra 93,3 % en escalada de privilegios a más de 80 veces menos costo que Opus 4.7 (PrivEsc-LLM), y los modelos pequeños rinden bien clasificando CWE y severidad y generando comandos de Kali (KaliBench, CyberPal 2.0, Foundation-Sec-8B). Ojo: varias de esas comparaciones son contra GPT-4o o GPT-4o-mini, no contra la frontera de 2026.
- **Parches: frontera.** En AIxCC, Trail of Bits quedó segundo con Claude y GPT, y no encontré finalistas que parcharan con un modelo pequeño. Un paper concluye que los modelos de reparación ajustados están sobreestimados porque memorizan parches.
- **Rechazos de la frontera: datos contradictorios.** Un estudio de 400 corridas de pentest no registró rechazos persistentes tras reintentar; otro midió 12,2 % en tareas defensivas, y las palabras «exploit» o «payload» los multiplican por 2,72. Los programas de acceso para seguridad de OpenAI y Anthropic piden aprobación y no llegan en 24 horas. Por eso sirve tener un modelo abierto de respaldo.
- **Ajustar un modelo en 24 horas** no es realista para explotación. Mejor usar modelos ya ajustados: `fdtn-ai/Foundation-Sec-8B-Reasoning`, `DeepHat/DeepHat-V1-7B` y los que listó Mauricio.
- **Competidores:** XBOW usa modelos de frontera (GPT-5.5 desde junio de 2026). Novee dice usar modelos propios ajustados, pero no publica tamaño ni base.

## El argumento de producto que sí se sostiene

- **Las empresas pequeñas no hacen esto:** en Reino Unido solo 10 % de las microempresas y 21 % de las pequeñas hizo un pentest el último año; en EE. UU., 26 % de las pymes no hace pruebas regulares.
- **El código generado por IA es explotable:** cerca del 50 % de los backends generados por modelos que pasan sus tests son explotables en vivo (BaxBench).
- **Lo diferencial no es el modelo, es la prueba:** ningún hallazgo se reporta sin un exploit que lo confirme, y ningún parche se acepta si el exploit sigue funcionando o si se rompen los tests.

Frase propuesta: «Local por defecto para lo que ve tu código, frontera para lo que necesita razonar, y nada se reporta sin prueba ejecutable».
