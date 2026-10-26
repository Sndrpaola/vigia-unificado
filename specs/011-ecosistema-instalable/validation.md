# Validación011 — 2026-10-22

Implementación autorizada por «perfecto ahora modificalo» y continuada por «haz lo que quedo pendiente».

## Implementado

- Inicio de reloj sin CareEvent ficticio,60/90/120, cuenta regresiva, pausa/reanudación y cambio de intervalo. Tokens/generación/transacciones conservados. Crear dos veces rechaza sin reiniciar silenciosamente.
- Servicio local Flutter con flutter_local_notifications22.3.2/timezone0.11.2, permisos Android/iOS, horarios absolutos del servidor, cancelación al salir, supresión de registros obsoletos y límite60 pendientes. Función separada de Firebase; riesgos conservan push. Dispositivos nuevos registran modalidad local para postura; API permite actualizar modalidad propia. Migración0006 aplicada SOLO a demo aislada.
- Web índigo/fondos claros/tarjetas redondeadas y marca VIGIA compartida; modo oscuro conserva elección. Backend y planes007/010 únicos.
- Código Django en web/, Flutter en mobile/ y nodo en edge/. manage.py raíz delega al de web; requirements raíz incluye lock web. No se trasladaron DB real/.env/media ni entornos. Configuración normal apunta explícitamente a sus ubicaciones originales; demo usa .mobile-demo original. Traslado registrado en traslado.json. Migraciones mantienen labels/imports.
- Flutter separado en core, app, shared, notifications, features/auth, home, patients, medications, posture, subscription, profile, detection. Exports de compatibilidad en api.dart/care.dart/archivos de detección. Reloj, filtros, perfil y plan como componentes propios.
- Demo /descargar/ sirve únicamente APK fijo y explica servidor/IP. APK Android ARM64 debug actualizado; es prueba local con API inicial10.0.2.2:8000 editable en login. No es una distribución de producción.

## Evidencia ejecutada

- [173 tests Django OK](evidencia/django-tests.txt) en core.test_settings. Corrección del aislamiento de caché de login entre tests; ensayo de concurrencia SQLite reconoce que ambos escritores pueden solicitar reintento, verifica máximo1 y comprueba reintento secuencial más rechazo por cupo. No se alteró regla comercial para aprobar test ni se certifica backend productivo.
- [13 tests Flutter OK](evidencia/flutter-tests.txt), incluidos horarios con offset, eliminación de avisos antiguos, logout durante consulta y estado vacío/pausado. [Análisis sin incidencias](evidencia/analyze.txt).
- [APK compilado](evidencia/apk.txt), [web compilada](evidencia/web-build.txt), [check](evidencia/check.txt), [esquema sin diferencias](evidencia/schema.txt).91 plantillas compiladas después de ajustes de marca. Aviso firebase_core/Kotlin de compatibilidad futura no impidió build.
- Navegador: login demo_premium en app y web; plan Premium compartido; paciente inicialmente sin reloj → Crear recordatorio60 → cuenta regresiva → Pausar; web refleja pausa. Catálogo claro y suscripción oscura inspeccionados. [Reloj](evidencia/reloj-activo.png), [planes](evidencia/planes-web.png), [modo oscuro](evidencia/suscripcion-oscuro.png). No se activó cámara personal.
- Descarga accesible en192.168.1.9:8000/descargar/ desde navegador del Mac con dirección LAN; conexión desde un celular externo todavía no comprobada. La IP cambia al cambiar de red.

## Límites y pendientes

**iOS:** Xcode ausente, xcode-select apunta a /Library/Developer/CommandLineTools. Se detuvo el intento de build tras detectar ausencia para no continuar descargas. Código/puente y permisos escritos, sin build iOS exitoso ni IPA firmada. Requiere instalar Xcode, seleccionar herramientas, firma/desbloqueo/Developer Mode y dispositivo. No se adquirió cuenta ni publicó TestFlight.

**Dispositivos:** APK no instalado físicamente; notificación con pantalla bloqueada, reinicio/ahorro de batería y MediaPipe real en ambos SO pendientes. Pruebas simuladas no acreditan sonido/precisión. Actualizaciones desde web requieren reabrir app con red; un reloj ya vencido no genera ráfagas. No repetir alerta hasta una nueva ocurrencia. Revisión responsive completa/zoom/teclado restante y aceptación funcional pendientes.

**Tailwind:** [diagnóstico](evidencia/tailwind.txt). Comando ejecutado pero sin CSS nuevo debido a firma inválida del binario oficial sobre macOS27. Se conserva generado anterior; nuevas decisiones de diseño están en CSS semántico normal. Recompilar en runtime compatible antes de entrega productiva; no declarar build Tailwind aprobado.

**Externos:** servidor HTTPS remoto no definido, OAuth/Firebase/APNs de producción sin configurar ni comprobar. Sin migración de DB real, datos reales, tiendas, despliegue, commit ni push.

Verificación final adicional: /descargar/ devuelve200; HEAD /descargar/android.apk devuelve200, MIME Android y142904125 bytes. Enlaces locales de README/guías011 sin roturas.


## Reanudación iOS — 2026-10-22
Xcode27.1 (27A9275) instalado en /Applications/Xcode.app y seleccionado. El bloqueo anterior de ausencia de Xcode queda sustituido por preparación inicial: xcodebuild -checkFirstLaunchStatus indica licencia no aceptada. Se solicitó al propietario revisar/aceptar directamente en Xcode; el agente no aceptó términos. Flutter3.47.7 se restaura en .tooling/flutter (ignorado por Git), evitando depender de /tmp. Compilación y firma iOS siguen pendientes; no hay IPA nueva.

Flutter3.47.7 restaurado correctamente en .tooling/flutter; pub get completado. checkFirstLaunchStatus llegó a devolver salida vacía, pero devicectl/simctl rechazaron ejecución por licencia no aceptada (código69): el estado vacío no acredita aceptación de licencia ni disponibilidad de dispositivos. Se conserva bloqueo legal y no se aceptaron términos mediante herramientas.


## Xcode preparado — reanudación posterior22/10/2026
Licencia resuelta por propietario: devicectl/simctl ejecutan correctamente. Disponibles simuladores iPhone17/iPhone17Pro, runtime iOS26.4; no aparece dispositivo físico. Build iOS retomado con Flutter local, resolviendo dependencias SwiftPM. Se retiraron únicamente mobile/build/app/intermediates y outputs/apk duplicados para recuperar espacio; APK público de outputs/flutter-apk conservado. Resultado pendiente, no afirmar IPA/instalación física.


## iOS: licencia resuelta, disco insuficiente — 2026-10-22
Xcode27.1 ya permite devicectl/simctl. Solo simuladores iPhone17/17Pro (runtime26.4), sin iPhone físico. Build falló extrayendo Firebase/grpc por disco lleno (125MB disponibles). Se retiró únicamente mobile/build/ios del intento fallido, recuperando aproximadamente800MB. Se preparó CocoaPods mediante flutter.config.enable-swift-package-manager=false; pub get OK y el paquete SwiftPM generado quedó sin dependencias. Esto evita resolver módulos Firebase ajenos al uso actual; Podfile existente conserva FirebaseCore/Messaging y MediaPipe. No se ejecutó un nuevo build ni pod install con menos de1GB libre; propietario debe liberar8–10GB antes de reintentar. No IPA ni notificación física aprobadas.

El APK anterior ya no está en mobile/build/app/outputs/flutter-apk después de trabajar con los generados de Flutter; requiere regeneración y copia a ubicación de entrega estable cuando haya espacio. No presentar su enlace como descarga disponible hasta comprobar archivo.
