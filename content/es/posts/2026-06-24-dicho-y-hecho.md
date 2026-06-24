---
title: "Dicho y Hecho: un agente para rastrear promesas"
date: 2026-06-24
type: post
categories: [Proyectos]
tags: [agentes, ia, claude-code, openspec, python, railway]
---

Durante mucho tiempo me ha rondado por la cabeza lo barato que resulta hacer una promesa en público. Nadie vuelve a comprobar si los políticos, directivos de empresas o supuestos expertos en cualquier tema cumplieron las promesas o predicciones que dijeron. La IA me pareció la herramienta perfecta para automatizar ese seguimiento y después de un tiempo dándole vueltas me decidí a intentarlo.

## 🏗️ El sistema

"Dicho y Hecho" fue un sistema que rastrea promesas y predicciones en medios de comunicación: extrae el contenido, el autor y la fecha de vencimiento, y luego monitoriza si se cumplieron. La arquitectura tiene tres capas —datos y lógica de negocio, web pública, y agentes en background— diseñadas para evolucionar de forma independiente y fácilmente desplegable en [Railway](https://railway.app). **Un agente rastrea canales RSS en busca de promesas nuevas; otro monitoriza las que han vencido buscando evidencias de cumplimiento vía web search.** Ambos proponen cambios a una cola de revisión centralizada: nada se publica directamente, todo pasa primero por una revisión humana.

{{< figure src="/img/posts/dicho-y-hecho-arquitectura.svg" alt="Arquitectura de Dicho y Hecho" caption="Arquitectura de Dicho y Hecho" width="70%" >}}

Para el desarrollo usé Claude Code desde el principio, en modo vibe coding: dejé que la IA propusiera la arquitectura en Python y fui construyendo encima sin preocuparme demasiado de los internals. A mitad del proceso integré **[OpenSpec](https://openspec.dev)**, que me resultó muy útil para refinar ideas, identificar casos límite e inconsistencias, y revisar los planes de implementación detalladamente antes de ejecutarlos. Como no tenía una opinión fuerte sobre la implementación, tampoco exploré todo lo que OpenSpec podría haber dado, pero aun así cambió bastante la forma de trabajar.

## 🎓 Cosas que he aprendido

El sistema estuvo en marcha unas cuatro o cinco semanas. De ese tiempo me llevo cuatro cosas:

**El coste de los agentes depende mucho del modelo.** Procesar decenas de noticias al día con Sonnet via API tiene un coste mensual significativo para un proyecto personal. Haiku lo hace viable económicamente, pero los resultados son algo peores. Al final la conclusión es clara: o pagas lo que cuesta hacerlo lo mejor posible, o asumes que alguien tendrá que revisar el trabajo.

**Los falsos positivos fueron el problema más persistente.** Anuncios de eventos, predicciones sin fecha concreta, declaraciones ambiguas. Con Haiku llegaba demasiado ruido; con Sonnet, menos, pero seguía llegando. Revisé el prompt varias veces y fue mejorando, pero nunca lo suficiente como para no tener que mirar la cola cada día. La tarea de análisis requiere de un esfuerzo importante de comprensión, y eso hoy en día un modelo sencillo no lo puede solucionar consistentemente.

**La detección de duplicados la subestimé.** La misma noticia en distintos medios o recogida en diferentes días aparecía varias veces como promesas distintas. Con el inconveniente de incrementar los costes, acabé integrando también IA para detectar duplicados entre las propuestas pendientes. Funcionó mucho mejor que el enfoque puramente sintáctico que intenté inicialmente.

**Los tests generados con IA no siempre cubren todos los casos.** El sistema sufrió errores en runtime por respuestas del API inconsistentes con la estructura de datos esperada, sobre todo en longitudes de campos. Cosas que los tests, generados también con ayuda de IA, no habían anticipado y que aparecieron cuando el sistema llevaba un rato corriendo en producción. Algo que debería haber sido fácilmente identificable se escapó a "producción" por carencias en la generación por defecto de la IA.

## 📊 Resultados

Al final, como ya he dicho, tuve funcionando el sistema sólo algunas semanas. La realidad es que requería una revisión diaria de la cola —nuevas propuestas y promesas vencidas— y acabé abandonándolo y desinstalándolo al poco tiempo. No porque no funcionara técnicamente, sino porque el coste de atención que requería no era sostenible para mi.

> la IA ha eliminado en buena parte la barrera técnica de construir algo, pero si el resultado no está completamente automatizado, sigue requiriendo un esfuerzo de mantenimiento que muchos proyectos personales no pueden asumir.

El abandono ya no viene de "no tengo tiempo de hacerlo", sino de "no tengo tiempo de mantenerlo vivo". Un coste que ya estaba ahí siempre, pero que ahora destacaba como principal barrera.

De todas formas, personalmente el proyecto lo considero un éxito. Como PoC, cumplió lo que tenía que cumplir: aprendí a montar un sistema completo con varios agentes IA trabajando en paralelo, entendí mejor la necesidad y los problemas de incluir human-in-the-loop en ese tipo de pipelines, y comprobé de primera mano las ventajas —y los límites— de usar herramientas como Claude Code u [OpenSpec](https://openspec.dev) en el desarrollo. Para unas semanas de trabajo ocasional, no estuvo mal. Supongo que si estás leyendo esto te sonará familiar la historia, ¿verdad?
