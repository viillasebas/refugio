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

## Plan de Pruebas de Estrés

### Objetivo
- Evaluar la estabilidad y comportamiento del sistema bajo cargas extremas y condiciones límite.

### Alcance
- Componentes incluidos: API REST (Express), base de datos (MySQL/PostgreSQL), autenticación (JWT), endpoints críticos (mascotas, solicitudes_adopcion), y almacenamiento de archivos.

### Escenarios críticos
- Carga máxima sostenida: mantener X usuarios concurrentes durante T horas.
- Picos cortos: ráfagas de peticiones que simulan campañas o picos de tráfico.
- Ramp-up hasta fallo: aumentar carga hasta que el sistema degrade o falle.
- Recuperación: verificar comportamiento tras reinicio o liberación de recursos.
- Degradación de dependencias: simular lentitud/caída de BD o almacenamiento.

### Perfiles de carga (ejemplo)
- Bajo: 100 usuarios concurrentes.
- Medio: 1.000 usuarios concurrentes.
- Alto: 5.000-10.000 usuarios concurrentes (según infra).
- Mix de operaciones: 70% lecturas (GET /api/mascotas), 30% escrituras (POST /api/solicitudes).

### Métricas y umbrales
- Latencia: P95 < 500 ms, P99 < 1200 ms (ajustar según SLA).
- Throughput: requests por segundo objetivo por endpoint.
- Tasa de errores: < 1% en escenarios aceptables.
- Uso de recursos: CPU < 80% (advertencia), RAM < 85% (crítico).
- Conexiones DB: no superar límites de pool y tiempos de espera aceptables.

### Herramientas recomendadas
- Generación de carga: k6 (recomendado), JMeter o Gatling.
- Monitoreo: Prometheus + Grafana, o APM (Datadog/NewRelic).
- Logs y trazas: EFK/ELK.

### Preparación y ejecución
1. Provisionar un entorno de staging representativo y aislarlo de producción.
2. Cargar dataset representativo y anonimizar datos sensibles.
3. Implementar scripts de carga con escenarios de ramp-up, sostenimiento y ramp-down.
4. Ejecutar una smoke test previa a cada iteración.
5. Ejecutar cada escenario 3 veces y capturar métricas, logs y trazas.

### Análisis y entregables
- Informe con gráficos de latencia, throughput y errores por escenario.
- Identificación de cuellos de botella y recomendaciones (caching, índices, escalado).
- Scripts y configuraciones usadas para reproducir las pruebas.

### Criterios de aceptación
- Métricas dentro de los umbrales definidos o plan de mitigación aprobado.
