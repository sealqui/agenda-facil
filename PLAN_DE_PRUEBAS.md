# Plan de Pruebas del Sistema — Agenda Fácil

**Proyecto:** Agenda Fácil — sistema de agendamiento de citas para consultorios pequeños (caso base: consultorio odontológico)
**Autor:** Sergio Alsina Quimbayo · Trabajo individual
**Curso:** Ingeniería de Software

## 1. Propósito y alcance

Este plan define qué se va a probar, cómo y con qué criterios de aceptación, siguiendo el acuerdo previo entre "cliente" (el consultorio) y "desarrollador" (yo) que quedó plasmado en la definición del proyecto: reemplazar la libreta de papel por un sistema digital de citas, sin perder disponibilidad ni control cuando falla el internet.

El plan cubre los tres módulos definidos en el alcance del proyecto:

- Agenda en línea (crear, confirmar, reprogramar, cancelar citas).
- Notificaciones automáticas (SMS / WhatsApp).
- Panel administrativo básico (ver agenda del día, bloquear horarios, reportes simples).

Quedan fuera de este plan, porque también quedaron fuera del alcance original: historia clínica completa, facturación electrónica y telemedicina.

## 2. Estrategia de pruebas

La calidad de un producto de software se mide en función de atributos verificables (ISO 9126: funcionalidad, confiabilidad, usabilidad, eficiencia, mantenibilidad, portabilidad), y las pruebas son la actividad que comprueba que esos atributos realmente se cumplen antes de que el sistema llegue al usuario final. Por eso el plan combina varios niveles de prueba en vez de uno solo:

| Nivel | Qué verifica | Cuándo se ejecuta | Responsable |
|---|---|---|---|
| Pruebas unitarias | Que cada función/endpoint aislado (validar horario, calcular disponibilidad, formatear un recordatorio) hace lo que debe | Durante cada sprint, antes de cerrar cada tarea | Rol de Desarrollo (yo) |
| Pruebas de integración | Que los módulos trabajan bien juntos: agenda ↔ base de datos, backend ↔ API de WhatsApp/SMS, frontend ↔ backend | Al final de cada sprint, sobre el incremento entregado | Rol de QA (yo) |
| Pruebas de sistema / aceptación | Que el flujo completo (paciente pide cita → se confirma → llega el recordatorio → se atiende) cumple los criterios que pidió el consultorio | Sprint 6, antes de la entrega piloto | Rol de QA + Product Owner (yo) |
| Pruebas de estrés / carga | Que el sistema no se cae con el uso real: varias citas simultáneas, envío masivo de recordatorios en la misma franja horaria | Sprint 6, en ambiente de pruebas | Rol de QA (yo) |
| Pruebas de usabilidad | Que la recepción (poca experiencia técnica) puede usar el panel sin capacitación extensa | Sprint 5-6, con el consultorio piloto | Product Owner (yo) + usuario piloto |

Esta combinación responde directamente al riesgo más crítico identificado en la definición del proyecto (fuga de datos de pacientes) y al riesgo de caída del servidor en horas pico: las pruebas de integración y de estrés existen específicamente para detectar esos dos escenarios antes de producción.

## 3. Casos de prueba

### 3.1 Requerimientos funcionales

| ID | Caso de prueba | Pasos | Resultado esperado | Tipo |
|---|---|---|---|---|
| CP-01 | Crear una cita disponible | 1. Paciente abre la agenda en línea. 2. Selecciona fecha/hora libre. 3. Confirma datos de contacto. | La cita queda registrada en estado "confirmada" y aparece en el panel administrativo | Funcional / integración |
| CP-02 | Bloquear doble reserva | 1. Dos pacientes intentan tomar el mismo horario casi al mismo tiempo. | Solo la primera solicitud se confirma; la segunda recibe "horario no disponible" y ve la agenda actualizada | Funcional / concurrencia |
| CP-03 | Reprogramar una cita | 1. Paciente busca su cita activa. 2. Elige nueva fecha/hora libre. 3. Confirma. | La cita anterior se libera automáticamente y la nueva queda confirmada; se envía notificación del cambio | Funcional |
| CP-04 | Cancelar una cita | 1. Paciente o recepción cancela una cita confirmada. | El horario vuelve a estar disponible de inmediato y se registra el motivo de cancelación | Funcional |
| CP-05 | Enviar recordatorio automático | 1. El sistema detecta una cita programada para el día siguiente. | Se dispara un SMS/WhatsApp con fecha, hora y nombre del profesional, 24 h antes | Integración (API externa) |
| CP-06 | Reintento si falla el envío | 1. La API de WhatsApp/SMS no responde. | El sistema reintenta el envío y registra el error para revisión de recepción | Integración / manejo de errores |
| CP-07 | Panel administrativo — agenda del día | 1. Recepción abre el panel al iniciar jornada. | Se muestra la lista de citas del día ordenada por hora, con estado de cada una | Funcional |
| CP-08 | Bloquear horario manual | 1. Recepción marca un bloque como no disponible (ej. cierre por mantenimiento). | Ese bloque deja de aparecer como disponible para nuevas citas | Funcional |
| CP-09 | Control de acceso al panel | 1. Un usuario sin sesión intenta entrar al panel administrativo. | El sistema deniega el acceso y solicita autenticación | Seguridad |

### 3.2 Requerimientos no funcionales

| ID | Caso de prueba | Condición | Resultado esperado | Tipo |
|---|---|---|---|---|
| CP-10 | Disponibilidad ante caída del servidor | Simular caída del servidor principal en horario de alta demanda | El monitoreo detecta la caída en menos de 5 minutos y el respaldo en la nube permite restablecer el servicio sin pérdida de citas ya confirmadas | Estrés / disponibilidad |
| CP-11 | Carga concurrente | 50 solicitudes de agendamiento simultáneas contra el mismo día | El sistema responde sin bloquearse ni duplicar horarios; tiempo de respuesta menor a 3 segundos por solicitud | Estrés / rendimiento |
| CP-12 | Cifrado de datos de pacientes | Revisar la base de datos y el tráfico entre frontend y backend | Los datos personales viajan y se almacenan cifrados; no son legibles en texto plano | Seguridad |
| CP-13 | Usabilidad del panel para recepción | Usuario piloto sin formación técnica realiza las tareas CP-01, CP-03, CP-07 sin ayuda | Completa las tres tareas en menos de 5 minutos combinados, sin errores críticos | Usabilidad |
| CP-14 | Portabilidad del acceso | Abrir la agenda en línea desde computador, tablet y celular | La interfaz se adapta y las funciones principales están disponibles en los tres dispositivos | Compatibilidad |

## 4. Evidencias simuladas de resultados

Estas evidencias corresponden a una corrida simulada de la batería de pruebas sobre el incremento del Sprint 6, tal como quedaría documentada antes de la entrega piloto:

| ID | Resultado | Observación |
|---|---|---|
| CP-01 | ✅ Aprobado | Cita creada y visible en panel en menos de 1 seg |
| CP-02 | ✅ Aprobado | Bloqueo de doble reserva funcionó en 20/20 intentos simultáneos |
| CP-03 | ✅ Aprobado | — |
| CP-04 | ✅ Aprobado | — |
| CP-05 | ✅ Aprobado | Recordatorio recibido 24 h antes en el 100% de la muestra (15 citas de prueba) |
| CP-06 | ⚠️ Aprobado con observación | El reintento funciona, pero tarda 10 min en notificar el fallo a recepción; se deja como mejora para el siguiente ciclo |
| CP-07 | ✅ Aprobado | — |
| CP-08 | ✅ Aprobado | — |
| CP-09 | ✅ Aprobado | Acceso denegado correctamente en 10/10 intentos sin sesión |
| CP-10 | ✅ Aprobado | Restablecimiento del servicio en 3 min 40 s tras la caída simulada |
| CP-11 | ⚠️ Aprobado con observación | Tiempo de respuesta promedio 2.4 s; 2 de 50 solicitudes superaron los 3 s en el pico de carga |
| CP-12 | ✅ Aprobado | Verificado con inspección del tráfico y de la base de datos |
| CP-13 | ✅ Aprobado | Usuario piloto completó las tres tareas en 4 min 10 s |
| CP-14 | ✅ Aprobado | Verificado en Chrome (escritorio), Android (Chrome) e iOS (Safari) |

**Cobertura:** 14 de 14 casos ejecutados, 12 aprobados sin observaciones y 2 aprobados con una observación menor que queda registrada como mejora para el ciclo posterior, no como bloqueante para la entrega.

## 5. Criterios de aceptación

El sistema se considera listo para pasar a producción cuando:

1. Todos los casos de prueba funcionales (CP-01 a CP-09) están aprobados sin observaciones críticas.
2. Los casos de seguridad (CP-09, CP-12) están aprobados sin excepción.
3. Las observaciones menores de rendimiento (CP-06, CP-11) quedan documentadas y priorizadas en el backlog de mejora post-entrega.
