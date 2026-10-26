# Organización del ecosistema VIGIA

- `web/`: manage.py, core, UsuarioApp, homeApp, PlanesApp, CuidadosApp, theme, templates, static, utils y requirements con lock. UI Django y adaptadores API comparten servicios y validación.
- `mobile/`: Flutter. app define tema/aplicación; core transporte/sesión; shared formularios y utilidades; features agrupa auth/home/patients/medications/posture/subscription/profile/detection. notifications contiene programación local y el plugin MediaPipe permanece en plugins/vigia_pose.
- `edge/`: procesamiento local de cámara fija y calibración.
- `docs/`, `specs/`, `prompts/`: documentación compartida. `manage.py` y requirements.txt de raíz son accesos compatibles, sin duplicar reglas.

Las ubicaciones originales `.env`, `db.sqlite3`, `media/`, `.mobile-demo/` y entornos se conservan. REPO_DIR identifica raíz y BASE_DIR la carpeta web. No mover secretos ni bases para ejecutar comandos. El traslado no renombra apps ni migraciones; [mapa de archivos](../specs/011-ecosistema-instalable/traslado.json).

Desde raíz: `.venv-mobile/bin/python manage.py check --settings=core.test_settings`. Desde web: `../.venv-mobile/bin/python manage.py check --settings=core.test_settings`. Tests: `manage.py test UsuarioApp homeApp PlanesApp CuidadosApp --settings=core.test_settings`. Nunca usar DB real para validaciones.

Flutter se opera desde mobile/. Sus entradas históricas lib/api.dart y lib/care.dart exportan las implementaciones por función para no romper consumidores. mobile/web/ es únicamente el lanzador de preview Flutter y no contiene la plataforma Django.
