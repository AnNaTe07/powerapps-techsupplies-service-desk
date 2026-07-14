# Sistema de Gestión de Incidencias

Aplicación desarrollada con **Microsoft Power Apps**, utilizando **SharePoint Online** como origen de datos y **Power Fx** para implementar la lógica de negocio.

---

# Descripción del proyecto

El **Sistema de Gestión de Incidencias** es una aplicación desarrollada con Microsoft Power Platform que simula el funcionamiento de una mesa de ayuda (*Service Desk*), permitiendo registrar, asignar y realizar el seguimiento de incidencias reportadas por los clientes.

La solución implementa un flujo de trabajo basado en roles, donde cada usuario dispone únicamente de las funciones correspondientes a sus responsabilidades dentro del proceso de gestión.

Su objetivo principal es centralizar el registro de incidencias, facilitar el seguimiento de cada solicitud y mejorar la organización del proceso de atención hasta su resolución.

---

# Capturas de la aplicación

## Pantalla de simulación de roles

![Simulación](assets/simulacion.png)

---

## Pantalla principal

![Inicio](assets/inicio_encargado.png)

---

## Detalle de la incidencia

![Detalle](assets/detalle.png)

---

## Edición de la incidencia

![Editar](assets/edición.png)

---

# Objetivos del proyecto

Durante el desarrollo se aplicaron los principales conceptos de Microsoft Power Platform para resolver un caso de negocio basado en un sistema de gestión de incidencias.

Los objetivos funcionales fueron:

- Registrar incidencias reportadas por clientes.
- Centralizar la información mediante SharePoint Online.
- Implementar un flujo de trabajo basado en roles.
- Gestionar el ciclo completo de vida de una incidencia.
- Asignar prioridades.
- Asignar responsables.
- Administrar el estado de cada incidencia.
- Permitir la consulta del historial.
- Diseñar una interfaz intuitiva y fácil de utilizar.

---

# Caso de negocio

Una empresa dedicada al soporte técnico recibe diariamente solicitudes relacionadas con inconvenientes técnicos, consultas y sugerencias.

Antes del desarrollo de esta aplicación, las incidencias podían registrarse mediante distintos canales, dificultando su seguimiento y control.

La solución desarrollada permite centralizar todas las solicitudes en un único sistema, asignar responsables, establecer prioridades y realizar el seguimiento de cada incidencia hasta su resolución.

---

# Tecnologías utilizadas

| Tecnología | Función |
|------------|---------|
| Microsoft Power Apps | Desarrollo de la aplicación |
| SharePoint Online | Almacenamiento de datos |
| Power Fx | Lógica de negocio |
| Controles Modernos | Interfaz de usuario |
| Variables globales y de contexto | Gestión del estado de la aplicación |

---

# Arquitectura de la solución

```text
Cliente
    │
    ▼
Power Apps
    │
    ▼
Power Fx
    │
    ▼
SharePoint Online
    │
    ▼
Lista de Incidencias
```

Toda la información se almacena en una lista de SharePoint utilizada como origen de datos para formularios, galerías y consultas de la aplicación.

---

# Modelo de datos

| Campo | Tipo | Descripción |
|--------|------|-------------|
| Cliente | Texto | Cliente que registra la incidencia |
| Incidencia | Texto | Título de la incidencia |
| Correo del cliente | Texto | Identifica al cliente |
| Fecha del reporte | Fecha y hora | Fecha de creación |
| Descripción | Texto | Descripción del problema |
| Categoría | Opción | Queja, Consulta o Sugerencia |
| Prioridad | Opción | Alta, Media o Baja |
| Estado | Opción | Abierta, En progreso o Resuelta |
| Fecha_Fin | Fecha y hora | Fecha de resolución |
| Comentarios | Texto | Observaciones adicionales |
| Responsable asignado | Texto | Técnico responsable |

---

# Flujo de trabajo

```text
Cliente registra incidencia
          │
          ▼
Estado = Abierta
          │
          ▼
Asignación de prioridad
          │
          ▼
Asignación de responsable
          │
          ▼
Estado = En progreso
          │
          ▼
Estado = Resuelta
          │
          ▼
Registro de Fecha_Fin
```

El estado **Abierta** se asigna automáticamente mediante un valor predeterminado configurado en SharePoint.

---

# Roles implementados

## Cliente

### Funciones

- Registrar incidencias.
- Consultar únicamente sus incidencias.
- Visualizar el detalle.
- Consultar el estado.

### Restricciones

No puede:

- modificar la prioridad;
- asignar responsables;
- cambiar el estado;
- registrar la fecha de resolución.

---

## Encargado

### Funciones

- Consultar todas las incidencias.
- Asignar prioridad.
- Asignar responsable.
- Administrar la información general.

### Restricciones

No realiza la resolución técnica.

---

## Responsable

### Funciones

- Actualizar el estado.
- Registrar la fecha de resolución.
- Completar comentarios finales.

---

# Navegación

```text
Simulación de Roles
        │
        ▼
Listado de Incidencias
        │
        ▼
Detalle
        │
        ▼
Editar
        │
        ▼
Guardar
        │
        ▼
Listado actualizado
```

---

# Variables principales

| Variable | Tipo | Función |
|----------|------|---------|
| varRol | Global | Rol seleccionado |
| varEmail | Global | Correo del usuario |
| varOrdenAsc | Global | Orden ascendente o descendente |
| varBuscar | Contexto | Visibilidad del buscador |
| varFiltroEstado | Global | Filtrado por estado |

---

# Funcionalidades implementadas

## Gestión de incidencias

- Registro de nuevas incidencias.
- Consulta de incidencias.
- Visualización del detalle.
- Actualización de información.
- Seguimiento del estado.

## Simulación de roles

Debido a las limitaciones del entorno académico, la aplicación incorpora una pantalla de simulación que permite representar distintos perfiles de usuario sin necesidad de múltiples cuentas de Microsoft 365.

## Búsqueda dinámica

Permite localizar incidencias por:

- Cliente.
- Incidencia.
- Prioridad.
- Estado.

La búsqueda admite coincidencias parciales y no distingue mayúsculas de minúsculas.

## Ordenamiento

La galería permite alternar entre orden ascendente y descendente según la fecha del reporte.

## Filtrado por estado

- Todas
- Abiertas
- En progreso
- Resueltas

---

# Diseño de interfaz

Durante el desarrollo se incorporaron mejoras de experiencia de usuario:

- Uso de contenedores.
- Header moderno con iconografía.
- Avatar generado automáticamente mediante iniciales.
- Badges para Estado y Prioridad.
- Paleta de colores consistente.
- Tipografía uniforme.
- Diseño adaptable.

---

# Decisiones de diseño

Se tomaron diversas decisiones para mejorar la experiencia del usuario:

- La prioridad únicamente es visible para el Encargado y el Responsable.
- El estado permanece visible para todos los roles.
- Toda incidencia se registra automáticamente con estado **Abierta**.
- El buscador se muestra únicamente cuando el usuario lo solicita mediante el icono correspondiente.

---

# Mejoras implementadas

Respecto de la versión inicial del proyecto se incorporaron:

- Rediseño completo de la interfaz.
- Optimización de la navegación.
- Búsqueda dinámica.
- Filtrado por estado.
- Ordenamiento por fecha.
- Avatares con iniciales.
- Badges para Estado y Prioridad.
- Organización mediante contenedores.
- Comentarios en las fórmulas principales.
- Renombrado de controles utilizando una nomenclatura descriptiva.
- Optimización del flujo de navegación.

---

# Conclusión

El Sistema de Gestión de Incidencias permitió aplicar los principales conceptos de Microsoft Power Platform mediante el desarrollo de una aplicación funcional basada en un escenario de negocio real.

Durante el proyecto se implementaron mecanismos de gestión por roles, formularios, validaciones, filtros, búsquedas, navegación entre pantallas e integración con SharePoint Online, utilizando **Power Fx** para desarrollar la lógica de negocio y mejorar la experiencia del usuario.
