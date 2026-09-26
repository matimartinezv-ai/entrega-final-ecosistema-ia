# Ecosistema de Automatización IA — Pipeline de Contenido con Control de Calidad (HITL)

**Entrega Final — Curso de Automatización No-Code (Make + n8n)**
Autor: Matías Martínez

## Qué es

Un ecosistema de automatización funcionando en vivo que resuelve un proceso de negocio de extremo a extremo: la **generación de contenido de marketing con control de calidad humano**. La IA redacta posts siguiendo las directrices privadas de la marca (RAG), un humano aprueba o rechaza con un clic, y solo lo aprobado se distribuye — con rutas de error que estabilizan el flujo y un dashboard público para monitorearlo.

**Stack (las 4 categorías obligatorias):**

| Categoría | Tecnología |
|---|---|
| Orquestador | **n8n** auto-hospedado (automation.controldata.cl) |
| Base de datos | **Airtable** — base "Centro de Comando Contenidos" (4 tablas vinculadas) |
| Procesamiento IA | **OpenAI GPT-4o-mini** con prompt estructurado + directrices RAG desde la DB |
| Canal de salida | **WhatsApp Cloud API** oficial de Meta (mensaje dinámico, formato internacional) |

## Flujo en una línea

`Trigger (15 min) → lee directrices (RAG) → toma ideas en estado "Generando" → valida datos → GPT redacta → guarda borrador (PAUSA HITL) → humano aprueba/rechaza en Airtable → filtro final → publica por WhatsApp → marca "Publicado" con fecha` — y cualquier fallo (dato faltante, API de IA caída, WhatsApp sin sesión) se desvía a la tabla **Log de errores** con vínculo al registro afectado.

## Contenido del repositorio

| Archivo | Criterio de la rúbrica |
|---|---|
| [`docs/01-diagrama-arquitectura.pdf`](docs/01-diagrama-arquitectura.pdf) | Mapa de arquitectura (triggers, routers, APIs, nodos IA, destino de datos) |
| [`docs/02-manual-operativo-datos.pdf`](docs/02-manual-operativo-datos.pdf) | Estructuras de datos: tablas vinculadas + esquemas JSON de transferencia |
| [`docs/03-matriz-costos-ia.pdf`](docs/03-matriz-costos-ia.pdf) | Optimización de costos: matriz de decisión por modelo y tarea |
| [`docs/04-seguridad-resiliencia.pdf`](docs/04-seguridad-resiliencia.pdf) | Seguridad y resiliencia: minimización de datos, rutas de error, HITL |
| [`flujo/pipeline-contenido-hitl.json`](flujo/pipeline-contenido-hitl.json) | JSON del workflow de n8n (16 nodos, credenciales no incluidas) |
| [`evidencias/`](evidencias/) | Capturas del flujo, la base, las ejecuciones y el WhatsApp recibido |

## Enlaces obligatorios

- **Dashboard de control (KPIs y tasa de errores)**: https://airtable.com/appsD44VEs1s5QgsA/shrtkH6oCJk6hhGjA
- **Base de control en modo lectura (Contenidos agrupada por estado)**: https://airtable.com/appsD44VEs1s5QgsA/shr7YQSXlckmfgBDJ
- **Video demo (3 min)**: _[PENDIENTE — se agrega el link al grabar]_

## Notas de seguridad

El JSON del flujo referencia credenciales por nombre (viven en el gestor de n8n, no en el repositorio) y el número de WhatsApp destinatario está enmascarado (`569XXXXXXXX`). Detalle completo en el documento 04.
