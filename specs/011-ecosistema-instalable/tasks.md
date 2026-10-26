# Tareas — 011

Estado actualizado22/10/2026 tras autorización de implementación. [Evidencia y límites](validation.md).

| Estado | ID / RF | Trabajo | Dependencia / terminado |
|---|---|---|---|
| [x] | T-011-01 /02 | Regresión del reloj vacío y contrato de inicio sin evento | Autorización; reproducir con paciente nuevo y documentar conducta |
| [x] | T-011-02 /02,04 | Inicio, intervalo, pausa/reanudación y conflictos en servicio/API/UI |01; pruebas propiedad, tokens, generación y reintentos |
| [ ] | T-011-03 /03 | Seleccionar dependencia y programar avisos locales en ambos SO |02; permisos, estados y prueba real de notificación |
| [ ] | T-011-04 /03,04 | Cancelación/reconciliación y coordinación con push |03; logout/archivo/otra cuenta/cambio web sin duplicados; migración si procede |
| [x] | T-011-05 /04 | Ensayo cuenta y plan web/app con backend único |02; Free/Plus/Premium y reducción de cupo verificadas |
| [ ] | T-011-06 /05 | Tokens y componentes web con estilo aprobado |Autorización; claro/oscuro/contraste/teclado/móvil y Tailwind |
| [x] | T-011-07 /06 | Inventario de rutas y manifiesto de traslado |Autorización; DB/secretos/entornos fuera del traslado automático |
| [x] | T-011-08 /06 | Separar web/ y modularizar Flutter por función |07; imports, comandos, assets, enlaces y pruebas sin regresión |
| [ ] | T-011-09 /01 | Preparar APK y conexión desde Android real |02–08; instalación y login con servidor accesible |
| [ ] | T-011-10 /01 | Build iOS y prueba en iPhone firmado |02–08; cuenta/firma/dispositivo disponibles; sin publicación implícita |
| [ ] | T-011-11 /01–06 | Validación integrada y guía de entrega |09–10; alarmas con pantalla bloqueada, cámara dual sin regresión y límites honestos |

Bloqueos externos: destino remoto no definido; firma/distribución Apple y dispositivos no verificados. Documentar evidencia por plataforma, no marcar tareas terminadas con pruebas sintéticas solamente. Siguiente paso: validación física de alarmas/cámara y completar iOS con Xcode/firma. Implementación ya autorizada.


## Autorización22/10/2026
El usuario indica «perfecto ahora modificalo»: implementación completa011 autorizada. Los estados documentales anteriores son antecedentes; no autorización de producción/tiendas ni migración real.


## Tareas parcialmente implementadas

T03/04: código y pruebas de planificación/cancelación/modalidad push terminados; notificación real y coexistencia física pendientes. T06: diseño aplicado y navegador claro/oscuro; Tailwind bloqueado por binario oficial y revisión responsive completa pendiente. T09: APK y descarga LAN disponibles; falta instalación Android física. T10: bloqueada por Xcode/firma/dispositivo. T11: pruebas automáticas y guía completas; integración física pendiente. Se mantienen abiertas por sus condiciones de finalización.
