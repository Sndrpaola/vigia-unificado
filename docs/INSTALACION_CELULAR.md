# Instalar y probar VIGIA

Estado25/10/2026: preview actualizada; APK ausente y pendiente de regenerar. No hay instalador actual disponible para teléfonos. Solo datos ficticios. Web/app usan la misma cuenta y los planes Free/Plus/Premium1/3/ilimitados.

## Android

1. Conecta celular y Mac a la misma Wi-Fi. Mantén el Mac encendido y la demo activa.
2. Abre [Descargar en la red local](http://192.168.1.9:8000/descargar/) desde el celular y descarga el APK. Android puede pedir autorización para instalar desde ese navegador. APK para ARM64, versión debug de prueba.
3. Abre VIGIA → «Servidor de pruebas» y guarda `http://192.168.1.9:8000`.
4. Entra con usuario `demo_premium` y contraseña `VigiaDemo-2026!`. También existen demo_free/demo_plus con la misma contraseña ficticia. Tu cuenta de producción no se copia a esta demo.
5. Posturas → Reloj de cuidados → paciente → Crear recordatorio →60/90/120. Pulsa «Activar avisos en este teléfono», concede notificaciones y, si lo solicitas, alarmas exactas. Si no se concede exactitud, el horario puede ser aproximado. Sonido sujeto a ajustes del teléfono. «Pausar», «Reanudar» y «Cambiar intervalo» guardan en servidor. Crear reloj no registra un cuidado realizado.

El APK se entregará en artifacts/android/VIGIA-android-prueba.apk tras ejecutar mobile/tool/build_android.sh; la descarga solo se muestra cuando existe el archivo. La descarga no equivale a prueba física aprobada: verificar recepción con pantalla bloqueada y luego pausa/logout, evitando datos reales. La app cancela avisos al cerrar sesión; cambios remotos necesitan conexión y volver a abrir la app. Avisos locales del reloj no necesitan Firebase; monitoreo y otros push requieren configuración externa.

La IP192.168.1.9 es la observada al preparar esta entrega y puede cambiar. Si no conecta, revisar IP y aislamiento Wi-Fi/firewall; no desactivar protecciones a ciegas. La red de otra ubicación puede bloquear comunicación entre equipos. Para uso fuera de Wi-Fi local hace falta un backend HTTPS accesible y su despliegue propio, todavía no preparado.

## Reiniciar demo

Desde raíz, con dependencias ya preparadas y sustituyendo IP si cambia:

```sh
VIGIA_DEMO_HOSTS=192.168.1.9 .venv-mobile/bin/python manage.py runserver 0.0.0.0:8000 --settings=core.mobile_demo_settings --noreload
```

La DB demo ya tiene migración0006. No aplicar migraciones en DB real para esta prueba. Abre http://127.0.0.1:8000/mobile/ para preview o /planes/ para web; preview web no ejecuta alarmas nativas ni MediaPipe telefónico.

## iPhone

No hay una IPA instalable todavía. Xcode27.1 ya está instalado y seleccionado. La licencia ya está resuelta y hay simuladores disponibles. La compilación para simulador fue exitosa23/10; artifacts/ios-simulator/Runner.app contiene el diseño anterior. No se pudo completar ejecución del simulador por espacio y no existe instalación física. Liberar espacio suficiente (8–10GB recomendados), recompilar el diseño25/10 y conectar un iPhone con firma de desarrollo. Para distribuir mediante TestFlight hace falta cuenta/configuración Apple y aprobación correspondiente. No se han publicado apps ni creado perfiles externos. Código Flutter/iOS preparado; compilación de la actualización25/10, permisos, alarma y MediaPipe iOS físicos siguen pendientes.

[Validación y bloqueos](../specs/011-ecosistema-instalable/validation.md).
