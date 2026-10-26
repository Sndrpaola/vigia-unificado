# VIGIA móvil

Flutter para Android/iOS con API Django compartida, conservando registro en web y login de la misma cuenta. [Instalar y probar](../docs/INSTALACION_CELULAR.md) · [Organización](../docs/ORGANIZACION.md) · [Resultados](../specs/011-ecosistema-instalable/validation.md).

lib/app y lib/core contienen aplicación/tema y transporte/sesión. lib/features separa auth, home, patients, medications, posture, profile, subscription y detection; lib/shared tiene formularios y utilidades. lib/notifications programa avisos locales. plugins/vigia_pose integra MediaPipe. Preview25/10 actualizada. APK pendiente de regeneración; iOS compiló para simulador23/10 con diseño anterior, sin IPA física. Ambos paquetes requieren recompilar para incluir esta actualización. La carpeta web/ de Flutter sirve para preview, mientras ../web/ contiene Django.

Desde esta carpeta: flutter pub get, flutter analyze, flutter test; flutter build apk --debug --target-platform android-arm64 --dart-define=API_URL=http://10.0.2.2:8000. SDK local estable: ../.tooling/flutter/bin/flutter (Flutter3.47.7, ignorado por Git). El SDK temporal anterior en /tmp fue eliminado. flutter build ios --simulator --debug --no-codesign requiere Xcode. No publicar ni firmar como producción con claves debug.
