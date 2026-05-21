# Берём за основу официальный образ Python версии 3.10
FROM python:3.10
# Устанавливаем рабочую директорию внутри контейнера
WORKDIR /app
# Копируем файл зависимостей внутрь контейнера
COPY requirements.txt .
# Устанавливаем все библиотеки из requirements.txt
RUN pip install -r requirements.txt --no-cache-dir
# Копируем весь остальной код проекта в контейнер
COPY . .
# Собираем статические файлы (CSS, JS) в одну папку для Nginx
RUN python manage.py collectstatic --noinput
# Открываем порт 8000 для внешних подключений
EXPOSE 8000
# Команда запуска приложения через Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "kittygram_backend.wsgi"]