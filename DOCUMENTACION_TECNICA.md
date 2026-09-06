# Documentación Técnica — Agenda Fácil

**Autor:** Sergio Alsina Quimbayo · Trabajo individual
**Curso:** Ingeniería de Software

## 1. Descripción general del sistema

Agenda Fácil es un sistema de agendamiento de citas pensado para consultorios pequeños que hoy dependen de una libreta de papel y llamadas telefónicas. Reemplaza esa libreta por una base de datos centralizada, con confirmaciones y recordatorios automáticos, sin exigirle al consultorio contratar personal técnico adicional.

## 2. Arquitectura por capas

| Capa | Tecnología elegida | Rol dentro del sistema |
|---|---|---|
| Frontend (paciente y recepción) | React (web) / Flutter (si se necesita app móvil) | Interfaz donde el paciente agenda/reprograma/cancela y la recepción administra el día |
| Backend | Node.js con Express | Lógica de negocio: disponibilidad de horarios, reglas de reprogramación, control de acceso |
| Base de datos | PostgreSQL | Almacena pacientes, citas, horarios y el historial de cambios (línea base de cada cita) |
| Notificaciones | Twilio API / API de WhatsApp Business | Envío de confirmaciones y recordatorios automáticos 24 h antes de la cita |
| Hosting | AWS o Render | Disponibilidad del sistema y respaldo ante caídas |
| Repositorio de código | GitHub | Control de versiones, líneas base del código e historial de cambios |
| Gestión de tareas | Trello | Tablero Kanban del backlog y el flujo de trabajo (Backlog → Por hacer → En progreso → En revisión → Hecho) |
| Modelado y diseño | Figma (mockups de pantallas) / draw.io (diagramas UML) | Documentación visual del diseño antes de programar |

## 3. Justificación técnica de las tecnologías

**React / Flutter.** El paciente que agenda una cita no tiene por qué instalar nada complejo: necesita una interfaz simple y rápida. React cubre el caso web sin fricción; Flutter queda disponible si el consultorio pide una app nativa más adelante, sin rehacer la lógica de negocio del backend.

**Node.js con Express.** Es liviano, tiene una curva de aprendizaje corta y es el estándar de facto para construir APIs REST rápido, lo cual encaja con un proyecto de alcance acotado (12 semanas) desarrollado por una sola persona.

**PostgreSQL.** Las citas, los pacientes y los horarios son datos estructurados con relaciones claras (un paciente tiene muchas citas, una cita pertenece a un horario). Una base relacional robusta como PostgreSQL evita inconsistencias — por ejemplo, dos citas confirmadas en el mismo horario — mejor que una base no relacional.

**Twilio / API de WhatsApp.** El riesgo más común de una libreta de papel es que nadie avise a tiempo. Automatizar el recordatorio por el canal que el paciente ya revisa (SMS o WhatsApp) es lo que realmente resuelve el problema, no solo digitalizar la libreta.

**AWS / Render.** El riesgo identificado en la definición del proyecto fue la caída del servidor en el día de mayor demanda. Un proveedor en la nube con monitoreo y respaldo mitiga ese riesgo mejor que un servidor propio en el consultorio.

**GitHub.** Más allá de alojar el código, centraliza toda la documentación del proyecto (este mismo repositorio) y cada commit funciona como una línea base: si algo falla, se puede volver a una versión anterior sin perder el trabajo.

**Trello.** Elegido sobre Jira o Asana por ser gratuito, visual y con una curva de aprendizaje mínima — apropiado para un trabajo individual donde no hay que coordinar convenciones de equipo.

**Figma / draw.io.** Antes de programar, el diseño de pantallas (Figma) y los diagramas UML (draw.io) permiten validar la solución con el "cliente" (el consultorio) sin haber escrito una línea de código, evitando rehacer trabajo más caro después.

## 4. Modelo de datos (resumen)

- **Paciente:** id, nombre, teléfono, canal de contacto preferido (SMS/WhatsApp).
- **Profesional:** id, nombre, horario de atención.
- **Cita:** id, paciente_id, profesional_id, fecha, hora, estado (confirmada / reprogramada / cancelada), historial de cambios.
- **Notificación:** id, cita_id, canal, estado de envío, fecha de envío.

## 5. Calidad del software aplicada al proyecto

Siguiendo la norma ISO 9126, el sistema se diseñó priorizando estos atributos de calidad:

- **Funcionalidad:** cubre exactamente los casos de uso definidos en el alcance (agendar, confirmar, reprogramar, cancelar, notificar).
- **Confiabilidad:** manejo de reintentos en notificaciones y respaldo en la nube ante caídas.
- **Usabilidad:** interfaz simple para un usuario sin formación técnica (recepción del consultorio).
- **Eficiencia:** tiempos de respuesta menores a 3 segundos incluso en picos de carga (ver Plan de Pruebas, CP-11).
- **Mantenibilidad:** código versionado en GitHub con historial de cambios (línea base) documentado.
- **Portabilidad:** acceso funcional desde computador, tablet y celular (ver Plan de Pruebas, CP-14).

Las métricas de producto que se hicieron seguimiento durante el desarrollo fueron principalmente dinámicas: número de errores reportados durante las pruebas de cada sprint y tiempo de respuesta bajo carga.

## 6. Referencias

Sommerville, Ian. *Ingeniería de Software*. Pressman, Roger. *Ingeniería del Software: un enfoque práctico*. Material de las Unidades 1 a 4 del curso de Ingeniería de Software (PMI/PMBOK, calidad ISO 9126, métricas, pruebas y gestión de configuración).
