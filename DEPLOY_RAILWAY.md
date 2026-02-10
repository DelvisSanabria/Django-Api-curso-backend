# Despliegue en Railway (Guía rápida)

1. Conecta tu repositorio a Railway (Dashboard -> New Project -> Deploy from GitHub).
2. En **Variables** del proyecto añade las siguientes variables:
   - `SECRET_KEY` (ej: una cadena segura)
   - `DEBUG` -> `False`
   - `ALLOWED_HOSTS` -> `tudominio.com,rails.app,localhost` (separadas por comas)
   - *Railway añadirá `DATABASE_URL` al añadir un plugin PostgreSQL* ✅
3. Ajustes de Build (opcional): en Railway puedes usar un Build Command para ejecutar migraciones y collectstatic:
   ```
   pip install -r requirements.txt && python manage.py migrate --noinput && python manage.py collectstatic --noinput
   ```
4. Railway usa `Procfile`, hemos añadido uno con: `web: gunicorn firstry.wsgi --log-file -`.
5. Recomendaciones:
   - Asegúrate de que `requirements.txt` incluye `gunicorn`, `whitenoise`, `dj-database-url` y `psycopg2-binary`.
   - Ejecuta `python manage.py collectstatic --noinput` durante el build para servir archivos estáticos con WhiteNoise.

¡Listo! Una vez desplegado, revisa logs en Railway y habilita variables de entorno necesarias.

## Pruebas locales 💡
1. Copia `.env.example` a `.env` y completa las variables (o exporta las env vars en tu entorno).
2. Instala dependencias y ejecuta migraciones:
   ```bash
   pip install -r requirements.txt
   python manage.py migrate
   python manage.py collectstatic --noinput
   python manage.py runserver
   ```
3. Revisa que la app funciona en `http://127.0.0.1:8000`.
