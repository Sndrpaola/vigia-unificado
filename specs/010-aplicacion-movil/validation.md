# Validación 010 — estado al 2026-10-20

Entrega parcial, sin aceptación funcional ni publicación. La referencia AI Studio indicada el 20 de octubre redirige a autenticación Google; su diseño todavía no se ha podido inspeccionar.

## Evidencia ejecutada el 2026-10-19

- Django: 168 pruebas OK en `core.test_settings`, registro local `.work-010/full-tests.txt`. Un ensayo anterior de la suite base tuvo fallo intermitente en concurrencia SQLite; la ejecución completa posterior pasó. No acredita concurrencia en un backend productivo.
- `check`: sin problemas; `makemigrations --check --dry-run`: sin cambios detectados.
- Flutter: análisis sin problemas y tres pruebas OK antes de los ajustes finales; APK debug generado, registro `.work-010/flutter-apk.txt`.
- Edge: cinco pruebas sintéticas OK. MediaPipe0.10.35 cargó el modelo oficial y detectó cero personas en imagen vacía, registro `.work-010/mediapipe-smoke.txt`. No se probó cámara ni precisión de clasificación con personas.
- Navegador: login demo, agenda/registro realizado, pacientes, guías, historial y plan Premium observados. Monitoreo muestra ausencia de observaciones sin nodo. No sustituye prueba nativa.
- iOS: primer intento falló extrayendo artefactos por disco lleno. Reintento descargó SDK y llegó a resolver GoogleSignIn con Swift Package Manager; se detuvo por espacio disponible inferior a400MB. Sin compilación iOS exitosa ni IPA.

## Cambios posteriores todavía sin recompilar

Se corrigió borrado de asociación local de dispositivo al olvidar sesión y se añadió regresión Flutter; se ajustó singular de actividad pendiente. El 20 de octubre se retiró formulario/envío de signup móvil y se enlazó registro web `/accounts/signup/`, conservando login/MFA/recuperación e identidad Django compartida. El APK existente y la vista previa compilada son anteriores a estos cambios.

Al reanudar el20 de octubre, `/tmp/vigia-flutter-sdk/bin/dart` ya no existe y flutter/dart no están en PATH. Formato, análisis, cuatro tests y compilaciones finales quedan pendientes de restaurar SDK y espacio. No se afirma que los cambios posteriores hayan pasado las pruebas anteriores.

## Pendientes de producto/integración

Acceder a referencia AI Studio mediante sesión Google del usuario o recibir exportación/capturas; comparar pantallas antes de adaptar diseño. Google OAuth, Firebase/APNs y entrega real de push, rotación de token y recepción por plataforma pendientes. Colaboración entre cuentas pendiente de política explícita. Nodo necesita hardware/cámara, calibración y métricas reales; no hay detección de caídas ni validación clínica. Android/iOS físicos, firma y aceptación funcional pendientes.

Migración0004 aplicada solo a demo/pruebas, no DB existente. Sin datos reales, despliegue, commits ni push. [Guía de prueba](../../docs/MOVIL_DESARROLLO.md).

## Inspección posterior de referencia — 2026-10-20

Bloqueo Google resuelto por el usuario. Pantallas recorridas y decisiones registradas en [referencia-ai-studio.md](referencia-ai-studio.md). Se mantiene evidencia histórica de compilaciones y límites; esta inspección no ejecutó pruebas nativas ni cámara. Detección dual y adaptación visual quedan documentadas en tareas18–23, pendientes de implementación.

## Implementación posterior de referencia y detección dual — 2026-10-20

Autorización humana explícita recibida. Código actualizado en mobile/lib/{main,care}.dart: paleta índigo, seis destinos, Inicio con acciones, Medicinas filtradas, Pacientes con búsqueda, Posturas con Guías/Reloj/Cámara y Perfil con identidad/seguridad web. Registro móvil remite a alta web. Mantiene Free/Plus/Premium del backend.

Cámara móvil en phone_pose_native.dart con plugin local vigia_pose (Java/Swift), camera0.12.1 y asset oficial MediaPipe. Se abre por acción explícita, sin audio, usa cámara trasera/capturas locales y referencias de sesión; elimina imagen al finalizar inferencia. No monitoriza en segundo plano ni detecta inmovilidad con capturas aisladas. La versión web explica que requiere móvil. Clasificador y pruebas Dart añadidas, todavía sin ejecutar por SDK ausente.

API /patients/<id>/phone-observations implementada; chequeo de cuenta/propiedad/Premium/cupo, whitelist4KB, antigüedad, UUID/idempotencia. Solo metadatos. Migración0005 permite origen nodo o teléfono, nunca ambos; riesgo vacío obligatorio para teléfono. Feed distingue origen. Las alertas continuas del nodo siguen independientes.

### Ejecutado

- Suite Django: **170 tests OK** con core.test_settings (10.520s), incluidos12 tests móviles. [Registro completo](evidencia/full-dual-tests.txt) y [API](evidencia/api-dual-tests.txt).
- check: sin problemas. makemigrations --check --dry-run: sin diferencias. Migración0005 aplicada solo en DB efímera de tests, no demo ni DB real.
- Sintaxis de Dart y Java analizada con Tree-sitter; Swift con swiftc -frontend -parse; Podfile con ruby -c: correctos. [Registro de sintaxis](evidencia/sintaxis-20261020.json). Esto NO equivale a análisis de tipos, resolución de dependencias, enlace ni ejecución.

### Bloqueo y pendientes concretos

El20 de octubre no existe SDK Flutter/Dart en /tmp ni PATH; al empezar había259MB libres. Se solicitó al usuario liberar varios GB (idealmente10GB) para reinstalar SDK y compilar. No se borraron archivos personales. pubspec.lock todavía corresponde a dependencias anteriores: resolver con pub get, revisar lock, ejecutar analyze/tests y build de cada plataforma antes de entregar otro APK. CocoaPods requerido para MediaPipe iOS; resolver versión/compatibilidad en compilación.

No se pudo inspeccionar visualmente la nueva UI ni probar cámara, permisos, orientación, precisión y ciclo de vida nativos. No hay APK/IPA nuevos; APK existente es anterior. No presentar los puentes nativos como funciones comprobadas en dispositivos. Campos adicionales/reportes/mapas de presión no implementados.


## Reanudación y compilación — 2026-10-21

Esta actualización reemplaza los bloqueos históricos de SDK y APK anteriores. Flutter3.47.7 restaurado en /tmp/vigia-flutter-sdk; pub get completado y lock actualizado. Análisis sin incidencias y **9 pruebas Flutter aprobadas**, incluida navegación/filtros a390×844. Evidencia en evidencia/analyze-20261021.txt y evidencia/test-20261021.txt. La suite Django previa conserva170 pruebas aprobadas; no se repitió porque no cambió el backend.

**APK debug Android ARM64 actualizado y compilado correctamente**, incluyendo plugin MediaPipe: mobile/build/app/outputs/flutter-apk/app-debug.apk. Comando: JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-22.jdk/Contents/Home /tmp/vigia-flutter-sdk/bin/flutter build apk --debug --target-platform android-arm64 --dart-define=API_URL=http://10.0.2.2:8000. El primer intento usó un Java de Android Studio cuya ruta desapareció; el reintento con Java22 instalado terminó correctamente. Aviso de compatibilidad futura de Kotlin en firebase_core, sin impedir build. No equivale a probar inferencia/cámara real.

Demo: migración0005 aplicada exclusivamente con core.mobile_demo_settings. Navegador: login ficticio demo_premium, Inicio con plan Premium/paciente/acciones, Medicinas con filtros, Posturas y pantalla dual de monitoreo comprobados. Vista web informa que MediaPipe telefónico requiere app nativa. Captura: evidencia/inicio-20261021.png. Se corrigió texto vacío de observaciones para explicar teléfono o cámara fija.

iOS sigue **sin compilación exitosa**: SDK iOS ausente y menos de1GB libre al cierre de compilación Android; no se descargaron más artefactos para evitar llenar disco. Requiere liberar varios GB (recomendados10GB), resolver CocoaPods y compilar iOS. Pendientes pruebas físicas Android/iOS, calibración y precisión, coexistencia real de cámaras, OAuth/Firebase/APNs y firma. No hay IPA ni despliegue ni migración de DB real. T18/20/21/22 permanecen abiertas por sus criterios nativos.

Build web final OK (32.3s), evidencia/web-20261021.txt. Retirados únicamente mobile/build/app/intermediates regenerables al finalizar para recuperar espacio; APK y vista previa conservados.


## Verificación vigente — 25/10/2026

Refinamiento de la referencia AI Studio dentro del alcance010/011 autorizado. Se conservan las seis secciones y funciones existentes; tema índigo/lavanda, paciente, acciones, agenda, Posturas y planes se acercan al prototipo. Catálogo móvil leído desde PlanesApp (Free/Plus/Premium,1/3/ilimitados; precios/beneficios sin duplicarlos en Dart). No migraciones ni contratación móvil nuevas.

- `.tooling/flutter/bin/flutter analyze` desde mobile: sin incidencias,5.1s. [Registro](evidencia/20261025/analyze.txt).
- `flutter test`:15 pruebas OK, apertura de ambos botones a URL sin query y navegación completa a320px incluidas. [Registro](evidencia/20261025/flutter-tests.txt).
- `.venv-mobile/bin/python manage.py test UsuarioApp homeApp PlanesApp CuidadosApp --settings=core.test_settings`:174 pruebas OK,10.991s. [Registro](evidencia/20261025/django-tests.txt). Subconjunto móvil:16 OK ([API](evidencia/20261025/api-tests.txt)).
- Build web OK,22s. [Registro](evidencia/20261025/web-build.txt). Preview demo en /mobile/, datos ficticios. No cambios de CSS/Tailwind en este ajuste.
- Navegador390×844: Inicio y Planes inspeccionados. Al pulsar «Cambiar plan» se abrió una pestaña /planes/, sin credenciales en URL; catálogo web Free Gratis/Plus$4.990/Premium$9.990 y1/3/ilimitados comprobado. Web pide su propia sesión; no se comparte token por URL ni se contrata un plan en esta prueba. Capturas [Inicio](evidencia/20261025/inicio-390.png), [Planes](evidencia/20261025/planes-390.png), [portal](evidencia/20261025/portal-web-390.png). Ancho320 comprobado con widget test; no captura de navegador320.

**Paquetes/dispositivos:** iOS compiló para simulador el23/10 (ver validación011), pero artifacts/ios-simulator/Runner.app es anterior a este diseño. No IPA física ni firma configurada. APK ausente y pendiente de regenerar mediante mobile/tool/build_android.sh. No se recompilaron paquetes25/10: aproximadamente1GB libre al cierre. No instalar ni presentar artefactos antiguos como esta versión. Cámara MediaPipe y alarmas físicas Android/iOS conservan sus pendientes; preview no los verifica. Sin despliegue, commit, push ni migración de base real. Próximo paso: espacio suficiente, recompilar Android/iOS y validar en teléfonos.
