# Gestión Post-Proyecto — Agenda Fácil

**Autor:** Sergio Alsina Quimbayo · Trabajo individual
**Curso:** Ingeniería de Software

## 1. Por qué es necesaria una etapa post-proyecto

Entregar el software funcionando no cierra el trabajo del ingeniero. El seguimiento del proyecto es un acto formal donde se evalúa el nuevo estado de las personas, la organización y el software mismo, y donde se decide qué pasa después: si el sistema se mantiene tal cual, si se le agregan funcionalidades, o si el rol del desarrollador termina en la entrega. Agenda Fácil define esa etapa desde ahora, para que el consultorio sepa exactamente qué esperar después del "Hecho" en el tablero de Trello.

## 2. Gestión de la configuración durante la operación

Cada cambio que se haga sobre Agenda Fácil después de la entrega sigue el mismo esquema de gestión de configuración usado durante el desarrollo:

| Rol | Responsabilidad en la etapa post-proyecto |
|---|---|
| Gestor de la configuración | Mantener el registro de versiones del sistema en producción y aprobar qué cambios se integran a la línea base |
| Coordinador | Verificar que la documentación (este repositorio) se actualice cada vez que cambia algo relevante del sistema |
| Responsable de los elementos | Confirmar que el código, la base de datos y la documentación estén siempre en la misma versión declarada |
| Gestor del cambio | Evaluar el impacto y el riesgo de cada solicitud de cambio antes de aprobarla |

En un proyecto individual, estos cuatro roles los asume la misma persona en momentos distintos, igual que se hizo con los roles de Scrum durante el desarrollo. Cada cambio aprobado genera una nueva línea base, registrada como un commit en GitHub con su propia descripción y fecha.

## 3. Estrategia de soporte

**Nivel 1 — Autoservicio.** El Manual de Usuario y las preguntas frecuentes de este repositorio resuelven las dudas más comunes de pacientes y recepción sin necesidad de contactar al desarrollador.

**Nivel 2 — Soporte directo.** Para fallas del sistema (el panel no carga, un recordatorio no llegó, un horario aparece bloqueado sin razón), la recepción reporta el caso por el canal acordado con el consultorio, indicando qué pasó y a qué hora. El objetivo de respuesta es el mismo día hábil para fallas que afectan el agendamiento.

**Nivel 3 — Mantenimiento correctivo.** Errores confirmados se corrigen, se prueban (siguiendo el mismo Plan de Pruebas) y se despliegan como una nueva versión documentada en el repositorio.

Es importante no confundir soporte con mantenimiento: el soporte resuelve dudas y reporta fallas de uso diario; el mantenimiento modifica el software mismo para corregir esas fallas o mejorar el sistema.

## 4. Monitoreo continuo

- **Disponibilidad del servidor:** monitoreo automático en la nube (AWS/Render) con alerta si el sistema deja de responder, para reaccionar antes de que el consultorio lo note.
- **Entrega de notificaciones:** revisión periódica de la tasa de éxito de los recordatorios por SMS/WhatsApp; una caída sostenida en esa tasa dispara una revisión de la integración con el proveedor.
- **Volumen de uso:** seguimiento de cuántas citas se agendan, reprograman y cancelan por semana, como base para decidir si el sistema necesita más capacidad.

## 5. Evaluación de resultados y aprendizaje post-proyecto

Al cierre de la primera versión en producción, se responde formalmente este checklist de aprendizaje:

- ¿Los tiempos y el alcance definidos en el Paso 1 se cumplieron?
- ¿Qué tan satisfecho quedó el consultorio con el sistema entregado?
- ¿Qué errores fueron los más costosos de corregir y cuál fue su origen?
- ¿La tecnología elegida (React/Flutter, Node.js, PostgreSQL, Twilio/WhatsApp) se comportó como se esperaba, o hay algo que cambiaría en un próximo proyecto similar?
- ¿Qué información de este proyecto sirve como base para futuros desarrollos del mismo tipo (otros consultorios pequeños)?

Estas respuestas quedan documentadas junto con el resto del proyecto, para que la experiencia de Agenda Fácil sea reutilizable si el consultorio pide nuevas funcionalidades o si el mismo sistema se adapta a otro negocio similar.

## 6. Nuevo estado después de la implementación

- **Del usuario (paciente y recepción):** se espera menos tiempo perdido en llamadas telefónicas y menos errores de doble reserva u olvidos, con la recepción dedicando ese tiempo a atención presencial en vez de administrar la libreta.
- **De la organización (el consultorio):** información centralizada y disponible en cualquier momento, sin depender de que una sola persona tenga la libreta a mano.
- **Del negocio:** una base ordenada de datos de citas que permite, más adelante, decisiones informadas (por ejemplo, qué horarios tienen más demanda) y la posibilidad de escalar el sistema a más profesionales o sedes.

## 7. Continuidad o cierre del rol del desarrollador

Al finalizar la entrega piloto se define explícitamente con el consultorio una de estas tres rutas, dejando constancia por escrito (correo o acta simple):

1. **Cierre del proyecto:** el sistema se entrega funcionando y el consultorio asume el uso diario, con soporte de Nivel 1 y 2 durante un periodo acordado.
2. **Mantenimiento continuo:** se define una ventana periódica (por ejemplo, mensual) para revisar el sistema, aplicar actualizaciones de seguridad y atender mejoras menores.
3. **Nuevas funcionalidades:** si el piloto resulta exitoso, se abre un nuevo ciclo de sprints para incorporar lo que quedó fuera del alcance inicial (historia clínica, facturación, telemedicina), partiendo del mismo repositorio y la misma línea base documentada aquí.
