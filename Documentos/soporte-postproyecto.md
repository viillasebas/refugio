# Soporte Post-Proyecto

## Objetivo
Definir el soporte, mantenimiento y continuidad del sistema del refugio después de su entrega.

## Soporte

| Nivel | Responsable | Respuesta | Resolución |
|---|---|---:|---:|
| L1 | Help Desk | 30 min | 4 h |
| L2 | Desarrollo | 2 h | 24 h |
| L3 | Liderazgo técnico | 1 h | 8 h |

## Contacto
- Email: soporte@refugio.com
- Teléfono: +57 315 123 4567
- WhatsApp: +57 319 456 7890
- Portal: refugio.com/soporte

## Incidencias
- P1 Crítica: sistema caído o pérdida de datos. RTO 1 h.
- P2 Alta: función principal afectada. RTO 4 h.
- P3 Media: función secundaria afectada. RTO 24 h.
- P4 Baja: error menor o mejora. RTO 7 días.

## Flujo
1. Registrar ticket.
2. Clasificar prioridad.
3. Diagnosticar causa.
4. Corregir en staging.
5. Validar con pruebas.
6. Desplegar a producción.
7. Confirmar cierre con el usuario.

## Mantenimiento
- Diario: revisar salud del sistema y logs.
- Semanal: limpieza temporal y verificación de integridad.
- Mensual: actualizar dependencias y revisar seguridad.
- Trimestral: auditoría y rendimiento.
- Anual: revisión global, licencias y plan de mejora.

## Backups
- Incremental: cada hora.
- Completo: diario.
- Retención: 30 días local y 1 año en nube.
- RTO: menor a 4 horas.
- RPO: menor a 1 hora.

```bash
mysqldump -u root refugio_db > /backups/refugio_$(date +%Y%m%d).sql
aws s3 cp /backups/refugio_*.sql s3://backup-bucket/
```

## Cambios
1. Crear RFC.
2. Revisar código.
3. Probar en staging.
4. Desplegar en ventana controlada.
5. Validar post-despliegue.
6. Documentar en CHANGELOG.

## Seguridad
- JWT para autenticación.
- MFA para administradores.
- TLS en tránsito.
- Roles y permisos.
- Auditoría de accesos.
- Validación de entradas.

```javascript
const helmet = require('helmet');
app.use(helmet());
```

## KPIs
| Métrica | Meta |
|---|---:|
| Disponibilidad | 99.5% |
| Tiempo de respuesta | < 2 s |
| Error rate | < 0.1% |
| Resolución P1 | < 4 h |
| Resolución P2 | < 24 h |

## SLA
- Disponibilidad mensual: 99.5%.
- 95% de solicitudes en menos de 2 segundos.
- Si no se cumple, se activa plan correctivo.

## Equipo
- 1 Administrador del sistema.
- 1 Desarrollador senior.
- 1 DevOps.
- 1 QA part-time.

## Escalación
- Lead Dev: +57 315 123 4567
- CTO: +57 316 123 4567
- Director: +57 310 123 4567

## Roadmap
- Q2 2026: despliegue y capacitación.
- Q3 2026: integración de pagos.
- Q4 2026: app móvil y notificaciones.
- Q1 2027: IA para matching de adopciones.

## Presupuesto
| Concepto | Costo |
|---|---:|
| Equipo técnico | COP 180.000.000 |
| Infraestructura | COP 24.000.000 |
| Herramientas | COP 20.000.000 |
| Capacitación | COP 5.000.000 |
| Total | COP 229.000.000 |

---

Versión 1.0 | Junio 2026 | Revisión: Diciembre 2026