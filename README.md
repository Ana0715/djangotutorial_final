## Полное веб‑приложение на Django с контейнеризацией через Docker. 

## Включает в себя:

* **Django**
* **PostgreSQL**
* **Docker & Docker Compose**
* **Nginx**
* **Админ‑панель Django**
* **Статические файлы**

## Установка и запуск

1. **Клонируйте репозиторий:**
- git clone https://github.com/Ana0715/djangotutorial_final.git
- cd djangotutorial_final
  
2. Создайте файл .env с переменными окружения:

3. Запустите контейнеры:
- docker compose up -d --build

4. Выполните миграции базы данных:
- docker compose exec web python manage.py migrate

5. Создайте суперпользователя Django:
- docker compose exec web python manage.py createsuperuser --username admin

6. Соберите статические файлы:
- docker compose exec web python manage.py collectstatic --noinput

Доступ к приложению

- Веб‑сайт: http://localhost или http://127.0.0.1
- Админ‑панель Django: http://localhost/admin
