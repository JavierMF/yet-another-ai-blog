---
title: "Cómo le enseñé a Claude a procesar mi inbox GTD"
date: 2026-06-26
type: post
categories: [Productividad]
tags: [GTD, Notion, Claude, Skills, MCP]
---

## 🧠 El problema

Tengo una memoria bastante mediocre. No en el sentido dramático de olvidar cosas importantes, sino en ese sentido cotidiano de tener la sensación permanente de que hay algo que se me escapa: una tarea que quería hacer esta semana, una fecha límite que se acerca sin que yo lo haya visto venir. Esa sensación me genera un estrés de fondo que no me gusta nada.

Hace bastante tiempo conocí [GTD](https://gettingthingsdone.com) —Getting Things Done, el sistema de David Allen— y lo usé durante una temporada para gestionar las tareas profesionales. Hace aproximadamente un año decidí recuperarlo para la vida personal usando [Notion](https://notion.so) como soporte. Me basé en [esta plantilla](https://app.notion.com/marketplace/templates/task-management-gtd-work-flow), la simplifiqué un poco, y el resultado funciona bien: proyectos, tareas individuales, y un inbox donde voy apuntando todo lo que entra para procesarlo después.

{{< figure src="/img/posts/gtd-notion-inbox.png" alt="Mi sistema GTD en Notion" caption="Mi sistema GTD en Notion" width="70%" >}}

El problema estaba justo ahí, en el "después". **El proceso de revisar el inbox y convertir cada nota en una tarea convenientemente etiquetada, asignada a un contexto, con sus fechas y su estado correcto... me resultaba tedioso**: no es que fuera difícil, es que requería demasiados pasos manuales creando, editando y eliminando items como para ir posponiendo ese momento de procesar. Y cuando uno pospone procesar el inbox en GTD, el inbox deja de ser un inbox y pasa a ser otro contenedor de caos, que es exactamente lo que querías evitar.

## 🤝 La solución

La solución la encontré con el [**conector de Notion en Claude**](https://developers.notion.com/guides/mcp/overview) para usar su MCP. Lo que hice fue enseñarle las bases de datos que uso, explicarle mi flujo de trabajo y los valores habituales de las propiedades, y probar un par de veces hasta que fue capaz de procesar el inbox como yo esperaba. Cuando el resultado fue consistente, le pedí convertirlo en una [skill](https://docs.anthropic.com/en/docs/claude-code/skills) donde registró todo lo que necesita: los IDs de las bases de datos, las plantillas de los JSON para crear o editar páginas, el flujo de trabajo, los valores por defecto, etc.[^1]

{{< figure src="/img/posts/gtd-notion-arquitectura.svg" alt="Arquitectura GTD con Claude y Notion MCP" width="60%" >}}

Ahora el proceso va así: le pido que procese el inbox, me muestra todas las entradas pendientes y para cada una me pregunta qué quiero hacer. La mayoría se convierten en tareas individuales. Algunas se convierten en proyectos, y entonces me pide que describa las subtareas. Para cualquier tarea, sabe qué valores usar por defecto y solo me pide confirmar la ubicación —en casa, fuera de casa, en el ordenador, en el móvil— porque eso depende de la tarea concreta y no hay forma de inferirlo.

Hay un detalle que me parece interesante: para los proyectos, Claude sabe que la primera tarea tiene que quedar en estado "Ready" —porque ya se puede ejecutar— pero el resto tienen que estar en "Blocked", porque normalmente dependen de que esa primera esté hecha. Es el tipo de lógica contextual que antes tenía que aplicar yo manualmente cada vez.

[^1]: La integración de Notion en Claude tiene algunas limitaciones — entre ellas, no puede eliminar páginas. Yo quería que al procesar cada entrada del inbox la eliminara para que quedara limpio. La solución fue añadir la integración con Zapier, que sí tiene esa capacidad. Un hack un poco cutre, pero funciona.

## ✅ El resultado

¿Qué ha cambiado en la práctica? Que ya proceso el inbox de verdad regularmente. Antes lo dejaba para después porque me daba pereza; ahora es una conversación de cinco minutos en la que básicamente voy respondiendo a preguntas concretas. El sistema hace lo que prometía hacer cuando lo leí por primera vez, que es sacar las cosas de la cabeza y ponerlas en un sitio de confianza. Solo que ahora el trabajo de ponerlas en ese sitio lo hace casi todo Claude.
