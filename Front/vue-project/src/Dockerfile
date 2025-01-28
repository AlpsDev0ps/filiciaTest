# ипользуем базовый образ
FROM python:3.12
# устанавливаем базовую директорию
WORKDIR /app
# копируем зависимости
COPY requirements.txt .
# устанавливаем
RUN pip install -r requirements.txt
# Копируем содержимое каталога
COPY . .
# открываем порт
EXPOSE 5000
#запускаем flask
CMD ["python", "app.py"]