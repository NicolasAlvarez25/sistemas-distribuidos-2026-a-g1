# Actividades — Semana 2, Sesión 2
## Sistemas Distribuidos — Microservicios, DDD y Bounded Contexts

---

| Campo | Detalle |
|---|---|
| **Estudiante** | Nicolás Álvarez |
| **Asignatura** | Sistemas Distribuidos |
| **Institución** | CORHUILA |
| **Semana** | Semana 2, Sesión 2 — Microservicios, DDD y Bounded Contexts |

---

## Actividad 1 — Identificar Subdominios

Para el proyecto **Gestión de Citas Inteligente** se identificaron tres subdominios principales, cada uno correspondiente a un microservicio del sistema.

---

### Subdominio 1 — Gestión de Usuarios
**Tipo:** Core

El subdominio central del sistema. Sin usuarios no hay citas. Gestiona el registro, autenticación y perfiles de todos los actores del sistema.

**Entidades principales:**

| Entidad | Descripción |
|---|---|
| Usuario | Persona registrada en el sistema con un rol asignado |
| Profesional | Usuario con rol PROFESIONAL que atiende citas |
| Cliente | Usuario con rol CLIENTE que agenda citas |

**Value Objects:**

| Value Object | Descripción |
|---|---|
| Email | Dirección de correo con formato validado, no tiene identidad propia |
| Contraseña | Cadena encriptada, se define por su valor no por un ID |
| Rol | Enumeración de tipo CLIENTE, PROFESIONAL o ADMINISTRADOR |
| Token JWT | Cadena que representa la sesión activa del usuario |

---

### Subdominio 2 — Gestión de Turnos
**Tipo:** Core

El subdominio más importante del negocio. Controla el agendamiento, disponibilidad y estado de las citas entre clientes y profesionales.

**Entidades principales:**

| Entidad | Descripción |
|---|---|
| Cita | Reserva de un turno entre un cliente y un profesional |
| Disponibilidad | Bloque de tiempo disponible de un profesional |
| HorarioSemanal | Configuración de horarios por día de la semana de un profesional |

**Value Objects:**

| Value Object | Descripción |
|---|---|
| FechaHora | Combinación de fecha y hora de una cita |
| EstadoCita | Enumeración: PENDIENTE, COMPLETADA, CANCELADA |
| Duracion | Tiempo estimado de duración de la cita en minutos |

---

### Subdominio 3 — Gestión de Notificaciones
**Tipo:** Supporting

Subdominio de soporte que complementa el flujo principal. No genera valor por sí solo pero mejora la experiencia del usuario al mantenerlo informado sobre sus citas.

**Entidades principales:**

| Entidad | Descripción |
|---|---|
| Notificacion | Registro de un mensaje enviado a un usuario |
| Recordatorio | Notificación programada para enviarse antes de una cita |

**Value Objects:**

| Value Object | Descripción |
|---|---|
| MensajeTexto | Contenido del mensaje enviado |
| EstadoNotificacion | Enumeración: PENDIENTE, ENVIADA, FALLIDA |
| TipoNotificacion | Enumeración: CONFIRMACION, RECORDATORIO, CANCELACION |

---

### Resumen de Subdominios

| Subdominio | Tipo | Microservicio |
|---|---|---|
| Gestión de Usuarios | Core | user-service |
| Gestión de Turnos | Core | turno-service |
| Gestión de Notificaciones | Supporting | notification-service |

---

## Actividad 2 — Context Map

El siguiente diagrama muestra los tres Bounded Contexts del sistema, sus relaciones y el tipo de comunicación entre ellos.

```
┌─────────────────────────────────────────────┐
│              👤 USUARIOS                    │
│                                             │
│  Entidades: Usuario, Profesional, Cliente   │
│  BD: PostgreSQL                             │
│  Expone: REST API + JWT                     │
└──────────────────────┬──────────────────────┘
                       │
                       │  JWT Token (user_id, rol)
                       │  REST API (verificar usuario)
                       │
          ┌────────────▼────────────┐
          │       📅 TURNOS         │
          │                         │
          │  Entidades: Cita,        │
          │  Disponibilidad,         │
          │  HorarioSemanal          │
          │  BD: PostgreSQL          │
          └────────────┬────────────┘
                       │
                       │  Eventos asincrónos
                       │  (cita_agendada, cita_cancelada)
                       │
          ┌────────────▼────────────┐
          │   🔔 NOTIFICACIONES     │
          │                         │
          │  Entidades: Notificacion,│
          │  Recordatorio            │
          │  BD: PostgreSQL          │
          └─────────────────────────┘
```

**Descripción de las relaciones:**

| Relación | Tipo | Datos compartidos |
|---|---|---|
| Usuarios → Turnos | REST síncrono | user_id, rol del usuario |
| Turnos → Notificaciones | Eventos asíncronos (Release 2) | cita_id, user_id, fecha, hora |

**Notas:**
- En Release 1 la comunicación entre Turnos y Notificaciones es síncrona (REST). La comunicación asíncrona con RabbitMQ se implementa en Release 2.
- El contexto de Notificaciones no se comunica directamente con Usuarios. Recibe el user_id desde Turnos y lo usa para enviar el mensaje.
- Cada contexto tiene su propia base de datos. No hay tablas compartidas entre microservicios.

---

## Actividad 3 — Mapeo de Bounded Contexts a Microservicios

| Bounded Context | Microservicio | Base de Datos | Comunicación | Release |
|---|---|---|---|---|
| Gestión de Usuarios | user-service | PostgreSQL | REST API + JWT | Release 1 |
| Gestión de Turnos | turno-service | PostgreSQL | REST API (síncrona) | Release 1 |
| Gestión de Notificaciones | notification-service | PostgreSQL | REST (R1) → RabbitMQ (R2) | Release 1 / Release 2 |

**Justificación de decisiones técnicas:**

PostgreSQL se usa en los tres microservicios porque los datos del sistema (usuarios, citas, notificaciones) son estructurados y requieren consistencia transaccional (ACID). En Release 2 se evaluará incorporar MongoDB para el historial de notificaciones donde la estructura flexible de documentos puede ser más conveniente.

La comunicación entre Turnos y Notificaciones evoluciona de síncrona a asíncrona en Release 2 porque el envío de notificaciones no debe bloquear el proceso de agendamiento. Si el servicio de notificaciones falla, la cita debe quedar registrada de todas formas.

---

## Referencias

- Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley.
- Newman, S. (2021). *Building Microservices*. O'Reilly Media.
- Material de clase — Semana 2, Sesión 2: Microservicios, DDD y Bounded Contexts. CORHUILA.
