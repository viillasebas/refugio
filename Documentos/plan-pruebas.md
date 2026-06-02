# Plan de Pruebas - Sistema del Refugio de Animales

## Introducción
Este documento define la estrategia de validación para asegurar el correcto funcionamiento, la seguridad y la integridad del Sistema de Información para el Refugio de Animales.

## Estrategia de Pruebas
Se aplicarán tres niveles de validación:
* **Pruebas unitarias:** Validación de funciones individuales y aisladas (por ejemplo, comprobar que el formato del correo electrónico ingresado sea válido).
* **Pruebas de integración:** Validación de la interacción entre módulos (por ejemplo, verificar que al aprobar una solicitud de adopción, el estado de la mascota cambie automáticamente a "Adoptado").
* **Pruebas funcionales:** Validación de las funcionalidades completas del sistema de cara al usuario (por ejemplo, completar el flujo completo desde que un adoptante se registra hasta que el veterinario le asigna una cita).

## Ambiente de Pruebas
* **Sistema operativo:** Windows / Linux
* **Backend:** Node.js / Express
* **Frontend:** React
* **Base de datos:** PostgreSQL

## Casos de Prueba Principales
1. **Registro de usuario:** Validación de la creación correcta de cuentas para adoptantes, voluntarios y veterinarios.
2. **Registro de mascota:** Verificación del ingreso de nuevos animales con sus datos básicos y fotografías.
3. **Procesamiento de solicitud:** Control de la generación y el envío digital del formulario de adopción.
4. **Actualización de historia clínica:** Validación de la persistencia de vacunas y diagnósticos médicos ingresados por el veterinario.