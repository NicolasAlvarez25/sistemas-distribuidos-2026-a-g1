# Actividades — Semana 1
## Sistemas Distribuidos

---

| Campo | Detalle |
|---|---|
| **Estudiante** | Nicolás Álvarez |
| **Asignatura** | Sistemas Distribuidos |
| **Institución** | CORHUILA |
| **Semana** | Semana 1 — Introducción a Sistemas Distribuidos |

---

## Actividad 1 — Identificar Sistemas Distribuidos

Se identificaron 3 aplicaciones de uso diario y se clasificaron según su arquitectura:

| Aplicación | Clasificación | Pistas |
|---|---|---|
| **WhatsApp** | Distribuida | Tiene app móvil, web y desktop. Los mensajes, llamadas y estados funcionan de forma independiente. Además, funciona parcialmente sin conexión a internet, lo que indica que diferentes componentes operan de manera autónoma. |
| **YouTube** | Distribuida | Las recomendaciones, el reproductor, los comentarios y las notificaciones son funcionalidades claramente independientes entre sí. Tiene app móvil y versión web, y cada función puede fallar sin afectar las demás. |
| **Spotify** | Distribuida | Funciona parcialmente offline con canciones descargadas. Tiene app móvil, web y desktop. La búsqueda, reproducción, playlists y podcasts parecen servicios completamente separados. |

**Conclusión:** Las tres aplicaciones son sistemas distribuidos. Las pistas más claras son la presencia de múltiples plataformas (móvil, web, desktop), el funcionamiento parcial sin internet y la independencia entre sus funcionalidades.

---

## Actividad 2 — Formación de Equipos

**Nombre del proyecto:** Gestión de Citas Inteligente

| Integrante | Rol |
|---|---|
| Yeison Scarpeta | Tech Lead / GitHub |
| Catalina Cortés | Backend Developer |
| Sofía Mendes | Frontend Developer |
| Nicolás Álvarez | DevOps / Docker Config |

Los roles fueron asignados según las habilidades de cada integrante. Yeison Scarpeta asume el liderazgo técnico y la gestión del repositorio, Catalina Cortés se encarga del desarrollo de los microservicios backend, Sofía Mendes del microfrontend en Angular, y Nicolás Álvarez de la configuración de contenedores con Docker y los ambientes de desarrollo.

---

## Actividad 3 — Brainstorming del Proyecto

### Idea principal: Gestión de Citas Inteligente

**¿Qué problema resuelve?**

La dificultad de agendar, gestionar y hacer seguimiento de citas de forma manual en consultorios, clínicas o servicios profesionales. El sistema elimina conflictos de horario, reduce el ausentismo mediante notificaciones automáticas y mejora la experiencia tanto del paciente como del profesional.

**¿Qué microservicios necesitaría?**

| Microservicio | Responsabilidad |
|---|---|
| Servicio de usuarios y autenticación | Registro, login y gestión de roles (paciente, profesional, administrador) |
| Servicio de agendamiento | Creación, modificación y cancelación de citas |
| Servicio de disponibilidad | Gestión de horarios y disponibilidad de los profesionales |
| Servicio de notificaciones | Envío de recordatorios y confirmaciones por correo o SMS |
| API Gateway | Punto de entrada único que enruta las peticiones a cada microservicio |

**¿Qué datos maneja?**

- Usuarios (pacientes y profesionales)
- Citas (fecha, hora, estado, motivo)
- Horarios de disponibilidad
- Notificaciones y recordatorios
- Historial de citas

---

## Referencias

- Tanenbaum, A. S. & Van Steen, M. (2017). *Distributed Systems: Principles and Paradigms*. Pearson.
- Material de clase — Semana 1: Introducción a Sistemas Distribuidos. CORHUILA.
