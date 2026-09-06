# Agenda Fácil

Sistema de agendamiento de citas para consultorios pequeños, desarrollado como proyecto individual para el curso de Ingeniería de Software.

**Autor:** Sergio Alsina Quimbayo

## El problema

Muchos consultorios pequeños todavía agendan citas con una libreta de papel y llamadas telefónicas. Eso genera errores: pacientes con el mismo horario, olvidos de avisar la cita, o nadie que sepa qué horarios quedan libres si la recepcionista falta. Agenda Fácil reemplaza esa libreta por un sistema digital que agenda, confirma, reprograma y cancela citas, con recordatorios automáticos por SMS/WhatsApp.

## Contenido de este repositorio

| Documento | Contenido |
|---|---|
| [PLAN_DE_PRUEBAS.md](./PLAN_DE_PRUEBAS.md) | Casos de prueba, estrategia de pruebas (unitarias, integración, estrés, usabilidad) y evidencias simuladas de resultados |
| [DOCUMENTACION_TECNICA.md](./DOCUMENTACION_TECNICA.md) | Arquitectura del sistema, modelo de datos y justificación de cada tecnología del stack |
| [MANUAL_USUARIO.md](./MANUAL_USUARIO.md) | Guía de uso para el paciente y para la recepción del consultorio |
| [GESTION_POST_PROYECTO.md](./GESTION_POST_PROYECTO.md) | Estrategia de soporte, mantenimiento, monitoreo y aprendizaje post-proyecto tras la entrega |

## Otros entregables del proyecto

- **Presentación del proyecto** (definición, metodología y stack): `Agenda_Facil_Presentacion.pptx`
- **Cronograma del proyecto** (Gantt de 7 sprints / 12 semanas y Sprint Backlog de 21 tareas, 192 horas): `Cronograma_AgendaFacil.xlsx`
- **Tablero Kanban del proyecto:** [trello.com/b/jgp37Fpg/agenda-facil](https://trello.com/b/jgp37Fpg/agenda-facil)

## Stack tecnológico (resumen)

Frontend en React/Flutter, backend en Node.js con Express, base de datos PostgreSQL, notificaciones vía Twilio/API de WhatsApp, hosting en AWS/Render, diseño en Figma y draw.io, gestión de tareas en Trello y control de versiones en este repositorio de GitHub. El detalle y la justificación de cada elección están en [DOCUMENTACION_TECNICA.md](./DOCUMENTACION_TECNICA.md).

## Metodología

Desarrollado con Scrum adaptado a trabajo individual: los cuatro roles (Product Owner, Scrum Master, Desarrollo, QA) los asume la misma persona en distintos momentos de cada sprint, sobre un backlog priorizado y entregas incrementales cada una o dos semanas.
