# Olist Analytics | Power BI

Proyecto personal para practicar análisis de datos con un caso de comercio electrónico. He utilizado el dataset público de Olist (Brasil) para preparar varias tablas, relacionarlas y construir un dashboard de ventas, entregas, satisfacción y calidad del dato.

La idea era ir más allá de montar gráficos: quería entender qué representa cada dato, comprobar los cálculos y documentar el trabajo.

**Accesos rápidos:** [Informe Power BI](powerbi/Olist_Analytics.pbix?raw=1) · [Documentación en PDF](docs/confluence/README.md) · [Jira y Scrum](docs/jira/README.md) · [Diccionario de métricas](docs/diccionario-metricas.md)

![Resumen de ventas](capturas/01-ventas.png)

## Qué incluye

| Página | Qué se puede consultar |
| --- | --- |
| **Ventas** | Importe de artículos, pedidos, clientes únicos, ticket medio, evolución mensual y principales categorías. |
| **Entregas** | Pedidos evaluables, retrasos, plazo medio y diferencias entre estados de Brasil. |
| **Satisfacción** | Distribución de puntuaciones de 1 a 5 y comparación entre entregas puntuales y retrasadas. |
| **Calidad del dato** | Fechas ausentes o incoherentes, pedidos sin artículos y valoraciones adicionales. |

### Entregas
![Página de entregas](capturas/02-entregas.png)

### Satisfacción
![Página de satisfacción](capturas/03-satisfaccion.png)

### Calidad del dato
![Página de auditoría](capturas/04-calidad-datos.png)

## Cómo lo he construido

- **Power Query:** importación de CSV y revisión de fechas, identificadores e importes. Tuve que corregir la interpretación de los decimales usando la configuración regional adecuada.
- **Modelo de datos:** relaciones entre pedidos, artículos, clientes, productos, vendedores y valoraciones; además de un calendario para filtrar por fecha de compra.
- **DAX:** medidas para ventas, pedidos distintos, ticket medio, porcentajes de retraso, días de entrega y valoraciones.
- **Comprobaciones:** página adicional de pruebas para contrastar recuentos y revisar indicadores.
- **Jira y Confluence:** organización retrospectiva del desarrollo, seguimiento de un sprint de cierre, documentación técnica y retrospectiva. Es una práctica individual, no una experiencia dentro de un equipo Scrum.

![Modelo de relaciones](capturas/05-modelo-datos.png)

## Comprobaciones realizadas

| Dato | Registros |
| --- | ---: |
| Pedidos | 99.441 |
| Líneas de artículos | 112.650 |
| Valoraciones | 99.224 |
| Pedidos diferentes valorados | 98.673 |
| Registros de valoración adicionales | 551 |

Encontré también ocho pedidos marcados como entregados sin fecha de entrega y 775 pedidos sin artículos asociados. No he eliminado estos registros automáticamente: algunos casos pueden tener una explicación válida.

## Organización del proyecto: Jira, Confluence y Scrum

También he utilizado este proyecto para practicar cómo organizar y documentar un desarrollo de datos, no solo cómo construir el informe.

### Jira

Organicé el trabajo en **3 épicas y 9 historias**. El desarrollo inicial de Power BI se documentó retrospectivamente. Para el cierre sí planifiqué un sprint con dos historias: revisar los indicadores y publicar el proyecto. Ambas quedaron terminadas y el sprint se cerró.

Las evidencias y una explicación breve están en la [documentación de Jira](docs/jira/README.md).

![Épicas terminadas en Jira](docs/jira/01-epicas.png)

![Resumen final de Jira](docs/jira/02-resumen.png)

![Historias del sprint de cierre](docs/jira/03-sprint.png)

*La captura muestra las dos historias en «Listo» antes de completar el sprint. La revisión y la retrospectiva recogen el cierre y el aprendizaje de esta entrega.*

### Confluence

Preparé **7 páginas** para explicar el origen de los datos, las transformaciones, el modelo, los indicadores, los problemas encontrados y la organización del trabajo. También documenté la revisión del sprint y una retrospectiva individual.

Los espacios de Atlassian se mantienen privados, así que he exportado las páginas a PDF para que puedan consultarse desde aquí sin iniciar sesión en Atlassian. Están reunidas también en el [índice de documentación](docs/confluence/README.md):

1. [Presentación del proyecto](docs/confluence/01-presentacion.pdf)
2. [Datos y preparación](docs/confluence/02-datos-modelo.pdf)
3. [Indicadores y dashboard](docs/confluence/03-dashboard.pdf)
4. [Pruebas y problemas encontrados](docs/confluence/04-validacion.pdf)
5. [Organización del trabajo](docs/confluence/05-organizacion.pdf)
6. [Revisión del Sprint 1](docs/confluence/06-revision-sprint.pdf)
7. [Retrospectiva del Sprint 1](docs/confluence/07-retrospectiva.pdf)

Para próximos proyectos quiero preparar el backlog desde el principio y comprobar las métricas conforme avance, en lugar de dejar tantas revisiones para el final.

## Abrir el proyecto

1. Descarga el archivo [`powerbi/Olist_Analytics.pbix`](powerbi/Olist_Analytics.pbix).
2. Ábrelo con **Power BI Desktop**. El informe conserva los datos importados en el momento de guardarlo.
3. Para actualizar las consultas, descarga los CSV desde el [dataset público de Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) y cambia las rutas locales de origen en Power Query. En mi equipo están configuradas bajo `E:\Olist`.

No se incluyen los CSV originales en este repositorio.

## Límites y próximos pasos

El **importe de artículos** suma los precios registrados; no representa ingresos netos de la plataforma ni necesariamente ventas completadas. El **porcentaje de retrasos** utiliza las entregas evaluables como denominador. Las **valoraciones** se analizan por registro, aunque algunos pedidos tienen más de una.

Quiero seguir mejorando la interpretación de pedidos cancelados, estudiar una única valoración por pedido cuando corresponda, aplicar tamaños mínimos de muestra en comparaciones territoriales y ampliar las pruebas. Los datos son históricos; el informe no representa la actividad actual de Olist.

En [`docs/diccionario-metricas.md`](docs/diccionario-metricas.md) explico las principales medidas y sus límites.

**Datos:** Brazilian E-Commerce Public Dataset by Olist. Proyecto personal, sin vinculación con Olist.
