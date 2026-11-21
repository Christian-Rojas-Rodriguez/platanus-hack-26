# Notas de Jaime: ¿la IA hizo crecer el ransomware? (cuarta investigación)

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Búsqueda del 21-11-2026 con prioridad mundial. Las cifras marcadas «secundaria» hay que abrirlas en su fuente antes de usarlas en el pitch.

## Respuesta corta

Es cierto solo a medias. El ransomware está en récord de volumen y la IA ya participa en ataques reales, pero ninguna fuente primaria mide qué parte del crecimiento se debe a la IA.

## Lo que se puede afirmar

- **Volumen récord.** Las víctimas publicadas en sitios de filtración crecieron 50 % en 2025 y el tercer trimestre de 2026 fue el más alto registrado, con 2.830 (Chainalysis, Check Point).
- **El negocio no creció igual.** Los pagos de 2025 cayeron 8 %, a unos 820 millones de USD, y el 69 % de las víctimas ya no paga (Chainalysis, Verizon DBIR 2026).
- **La capacidad de los modelos sí saltó.** En el rango de 32 pasos del instituto británico (sin defensores), los modelos pasaron de 1,7 pasos de media en 2024 (dato secundario) a resolverlo entero en 6 o 7 de cada 10 intentos en julio de 2026 (UK AISI con CAISI).
- **Casos reales, todavía pocos.** Un operador extorsionó a 17 organizaciones en un mes con un agente de código, sin cifrar (Anthropic, agosto de 2025). Un agente cifró 1.342 configuraciones de una víctima tras entrar por Langflow; un humano eligió el objetivo y aportó credenciales (JADEPUFFER, Sysdig, julio de 2026).
- **Baja la barrera de entrada.** Alguien sin capacidad técnica vendió kits de ransomware hechos con un modelo, a 400 a 1.200 USD, y el 67 % de 832 cuentas maliciosas vetadas por Anthropic usó IA para preparar herramientas.
- **DDoS:** sin efecto medido de la IA; los récords se explican por redes de dispositivos infectados y servicios de alquiler.

## Lo que no se debe afirmar

- Que el 80 % del ransomware usa IA: el estudio de MIT Sloan y Safe Security fue retirado.
- Que el ransomware creció por la IA: nadie lo cuantifica.
- Que PromptLock fue un ataque: era un prototipo académico de NYU.
- Que la IA hace más efectivo el phishing contra empresas: el DBIR 2026 no lo observa.
- Que los modelos ya comprometen redes bien defendidas: los rangos evaluados no tienen defensores.

## Ideas de proyecto que salieron

1. **Recuperación tras un agente destructor (la única que agregué al ranking, 65 puntos).** Un agente de código borra o cifra archivos por terminal, por error o por una inyección. Se mide cuánto recupera el deshacer nativo de Claude Code, Gemini CLI y OpenCode contra una capa de copias guardadas fuera del alcance del agente.
   - **Línea base real:** la documentación de Claude Code dice que no rastrea archivos cambiados solo por terminal; una encuesta de 435 trabajos sobre agentes no halló ninguno que reporte éxito de recuperación.
   - **Métrica:** porcentaje de archivos idénticos por hash tras restaurar, y porcentaje de trabajo legítimo que la restauración destruye.
   - **En contra:** el remedio son copias de seguridad, técnica conocida. El valor está en el número y en que las copias resistan al agente.
2. **Simulacro en vivo de ransomware para agentes defensores.** No hay benchmark donde un agente responda a un ransomware en vivo (SecRespond califica el plan como texto). No la agregué: escenarios y línea base serían nuestros, y el simulador roza una línea roja.
3. **Detector de cifrado en archivos de modelos de IA** (pesos, bases vectoriales), a partir de un ataque de 2026 que cifró ese tipo de archivos. No la agregué: su hipótesis central no la midió nadie.

## Sin verificar

Simuladores inofensivos de ransomware (quedó de memoria), cifras de borrados masivos por agentes en 2026 (secundarias), varias cifras de pagos y tiempos de explotación.
