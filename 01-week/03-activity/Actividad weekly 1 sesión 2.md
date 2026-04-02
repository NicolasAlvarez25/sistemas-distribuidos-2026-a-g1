# Actividades — Semana 2
## Sistemas Distribuidos — Fundamentos, Teorema CAP y Git

---

| Campo | Detalle |
|---|---|
| **Estudiante** | Nicolás Álvarez |
| **Asignatura** | Sistemas Distribuidos |
| **Institución** | CORHUILA |
| **Semana** | Semana 2 — Fundamentos de Sistemas Distribuidos |

---

## Actividad 1 — Análisis CAP

Para cada sistema se identifica la combinación del Teorema CAP que prioriza y se justifica la decisión:

| Sistema | Combinación CAP | Sacrifica | Justificación |
|---|---|---|---|
| **Sistema bancario de transferencias** | CP | Disponibilidad | La consistencia es crítica: si dos nodos muestran saldos diferentes puede haber fraude o pérdida de dinero. Se prefiere dejar de responder antes que dar información incorrecta. |
| **Feed de Twitter/X** | AP | Consistencia | Es aceptable que un usuario vea un tweet con unos segundos de retraso. Lo importante es que el sistema siempre responda. La consistencia eventual es suficiente. |
| **Sistema de reservas de cine** | CP | Disponibilidad | No se puede vender el mismo asiento dos veces. La consistencia es prioritaria para evitar conflictos de reserva, aunque el sistema tarde más en responder. |
| **DNS** | AP | Consistencia | El DNS siempre debe responder aunque devuelva una IP ligeramente desactualizada. La disponibilidad es lo más importante para que internet funcione. |

**Conclusión:** En sistemas distribuidos la Tolerancia a Particiones (P) siempre está presente porque la red siempre puede fallar. Por eso la decisión real es elegir entre Consistencia (C) o Disponibilidad (A) según el caso de uso. Los sistemas donde un dato incorrecto genera un problema grave (bancos, reservas) priorizan C. Los sistemas donde la velocidad de respuesta es más importante que la exactitud inmediata (redes sociales, DNS) priorizan A.

---

## Actividad 2 — Setup de Git

Cada miembro del equipo configuró Git con su nombre de usuario y correo de GitHub.

### Verificación de instalación y configuración

```powershell
git --version
git config --global user.name
git config --global user.email
```

### Captura — Verificación de Git configurado


![git config](./capturas/gitconfig.png)

---

## Actividad 3 — Repositorio del Proyecto

El Tech Lead del equipo (Yeison Scarpeta) creó y configuró el repositorio oficial del proyecto en GitHub con las ramas `main`, `qa` y `develop`, y agregó a todos los integrantes como colaboradores.

**Repositorio:** [https://github.com/sparyock/Gestion-De-Citas-Inteligente](https://github.com/sparyock/Gestion-De-Citas-Inteligente)

### Ramas configuradas

| Rama | Propósito |
|---|---|
| `main` | Código estable de producción |
| `qa` | Ambiente de pruebas y validación |
| `develop` | Integración de desarrollo activo |
| `feature/*` | Ramas individuales por funcionalidad |

### Integrantes del equipo agregados como colaboradores

| Integrante | Rol |
|---|---|
| Yeison Scarpeta | Tech Lead / GitHub |
| Catalina Cortés | Backend Developer |
| Sofía Mendes | Frontend Developer |
| Nicolás Álvarez | DevOps / Docker |

### Captura — Repositorio en GitHub


![repositorio github](./capturas/repoprincipal.png)

### Captura — Ramas configuradas


![ramas github](./capturas/ramas.png)

### Captura — README del proyecto


![readme github](./capturas/readmerepo.png)

---

## Referencias

- Brewer, E. (2000). *Towards Robust Distributed Systems*. PODC Keynote.
- Tanenbaum, A. S. & Van Steen, M. (2017). *Distributed Systems: Principles and Paradigms*. Pearson.
- Material de clase — Semana 2: Fundamentos de Sistemas Distribuidos. CORHUILA.
