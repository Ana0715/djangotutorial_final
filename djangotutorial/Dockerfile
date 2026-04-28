# Загружаем официальный образ Python версии 3.13
FROM python:3.13

# Запрещаем создавать .pyc файлы с кешем
ENV PYTHONDONTWRITEBYTECODE=1
# Запрещаем кешировать вывод
ENV PYTHONUNBUFFERED=1

# Задаем пользователя, группу и рабочую директорию
ENV USER=django_web
ENV GROUP=maintenance
ENV WORK_DIR="/usr/src/app"

# Создаем рабочую директорию
RUN mkdir -p ${WORK_DIR}
WORKDIR ${WORK_DIR}

# Создаем группу, юзера, добавляем юзера в группу и даем ему права доступа
RUN addgroup --system ${GROUP} && \
    adduser --system --ingroup ${GROUP} ${USER} --shell /bin/bash && \
    chown -R ${USER}:${GROUP} ${WORK_DIR}

# Передаём список зависимостей
COPY ./requirements.txt .

# Обновляем pip и устанавливаем зависимости
RUN pip install --no-cache-dir --upgrade pip && pip install --no-cache-dir -r requirements.txt

# Копируем файлы проекта
COPY . ${WORK_DIR}

# Создаём папку для статических файлов, если её нет
RUN mkdir -p ${WORK_DIR}/static/

# Даём доступ к папке со статикой
RUN chmod -R og+w ${WORK_DIR}/static/

# Переключаемся на созданного юзера
USER ${USER}

# Запускаем сервер разработки
# CMD [\
#     "gunicorn", \
#     "--bind", "0.0.0.0:8000", \
#     "--workers", "3", \
#     "--threads", "3", \
#     "djangotutorial.wsgi:application" \
#     ]
ENTRYPOINT [ "sh", "/usr/src/app/entrypoint.sh" ]