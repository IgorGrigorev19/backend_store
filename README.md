# Backend Store

Backend Store — это серверное приложение для интернет-магазина, предоставляющее API для работы с товарами, пользователями и заказами. Приложение легко запускается локально с помощью Docker и Docker Compose.

Для запуска клонируй репозиторий командой:

git clone https://github.com/IgorGrigorev19/backend_store.git  
cd backend_store

Далее создай файл .env в корне проекта со следующим содержимым:

PORT=3000  
DB_HOST=db  
DB_PORT=5432  
DB_USER=postgres  
DB_PASS=postgres  
DB_NAME=store_db  
JWT_SECRET=supersecretkey

После этого собери и запусти контейнеры:

docker compose up --build

Если используешь старую версию Docker Compose, запусти:

docker-compose up --build

После запуска приложение будет доступно по адресу http://localhost:3000  
Проверить работу можно запросом:

curl http://localhost:3000/health

Ожидаемый ответ: {"status":"ok"}

Ниже пример Dockerfile, который используется для сборки приложения:

FROM node:20-alpine  
WORKDIR /usr/src/app  
COPY package*.json ./  
RUN npm install  
COPY . .  
EXPOSE 3000  
CMD ["npm", "start"]

Также пример docker-compose.yml:

version: "3.8"  
services:  
  app:  
    build: .  
    container_name: backend_store_app  
    ports:  
      - "${PORT:-3000}:3000"  
    env_file: .env  
    depends_on:  
      - db  
    volumes:  
      - .:/usr/src/app  
    command: npm start  

  db:  
    image: postgres:15  
    container_name: backend_store_db  
    restart: always  
    environment:  
      POSTGRES_USER: ${DB_USER:-postgres}  
      POSTGRES_PASSWORD: ${DB_PASS:-postgres}  
      POSTGRES_DB: ${DB_NAME:-store_db}  
    ports:  
      - "5432:5432"  
    volumes:  
      - pgdata:/var/lib/postgresql/data  

volumes:  
  pgdata:

Проверить, что контейнеры работают:

docker ps

Остановить проект:

docker compose down

Удалить контейнеры и тома:

docker compose down -v

Автор проекта: Igor Grigorev  
GitHub: https://github.com/IgorGrigorev19  
Лицензия: MIT
