---
title: "Registrando recargas del coche en modo fácil"
date: 2026-06-30
type: post
categories: [Productividad]
tags: [Notion, Claude, Skills, Coche eléctrico, PDF]
images: ["/img/posts/recargas-notion.png"]
---

Desde que hace unos meses nos pasamos al coche eléctrico puro, la forma de "repostar" cambió completamente. No tenemos cargador en casa, por lo que nos toca cargar siempre en cargadores públicos. Pero con un eléctrico el patrón por nuestra parte no es el mismo que con los de combustión en gasolinera —parar cuando casi llegas a reserva a llenar— sino el opuesto: recargas pequeñas y frecuentes siempre que el coche está parado: cuando hay que dejarlo en un parking, cuando vas a un centro comercial o al cine, en el restaurante que tiene cargador, etc.

El resultado era un montón de cargos pequeños de muchos proveedores distintos, cada uno con su app y sus precios, y ninguna visión clara de cuánto había gastado en total ese mes.

## ⚡ Una solución ridículamente sencilla

La solución que monté para controlar el gasto casi da vergüenza de lo simple que es. El proceso completo:

1. Abro la app del banco, entro en el cargo de la recarga y pulso "compartir recibo" → genera un PDF para enviar.
2. Lo envío a Claude en el móvil, adjunto el PDF y escribo "Registra esta recarga".
3. Listo.

La skill que se lanza extrae desde el PDF el proveedor, la fecha y el importe, y lo añade a una base de datos en Notion. Desde ahí puedo ver fácilmente el total del mes, agrupar por proveedor, comparar meses.

{{< figure src="/img/posts/recargas-notion.png" alt="Registro de recargas en Notion" width="70%" >}}

Lo que me sorprendió fue lo sencillo que resultó el paso de extracción del PDF. Esperaba tener que ajustar el prompt, darle ejemplos, pasarle estructura o algo, pero no tuve que hacer nada: a la primera, Claude leyó el recibo y extrajo exactamente lo que necesitaba. No sé si porque los recibos bancarios tienen una estructura suficientemente predecible o simplemente Claude es muy listo, pero funcionó sin ninguna configuración especial.

## 🚗 Desarrollo desde el móvil

Algo especial de esta aplicación de la IA fue el "proceso de desarrollo", si es que se le puede llamar así. Estaba esperando en una consulta, aburrido, y se me ocurrió la idea. Empecé a explorar en un chat de Claude si sería posible algo así: qué campos tendría la base de datos, cómo extraería los datos del PDF, cómo lo conectaría con Notion.

Cuando me quise dar cuenta no solo estábamos discutiendo la idea: Claude había creado la base de datos en Notion, había procesado un par de recibos de prueba y había escrito la skill para poder repetirlo en el futuro. Todo en el tiempo que duró la espera.

## 📊 Lo que he descubierto

Por si alguien se lo pregunta: sí, estoy gastando algo más en recargas de lo que gastaba en gasolina. Pero no porque la electricidad salga cara —por kilómetro sale bastante más barato— sino porque desde que tenemos el coche eléctrico hacemos muchos más kilómetros. Es tan cómodo y divertido que hemos multiplicado las escapadas y los trayectos en coche. La contabilidad no miente, pero tampoco cuenta la historia completa.
