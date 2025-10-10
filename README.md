# 💾 Внутреннее хранилище (Backend Store)

![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?logo=docker&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-20.x-339933?logo=node.js&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15.x-336791?logo=postgresql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Active-success)

---

**Backend Store** — это внутреннее серверное приложение для интернет-магазина.  
Оно предоставляет REST API для управления товарами, пользователями и заказами.  
Приложение легко запускается локально с помощью **Docker** и **Docker Compose**.  

---

### 🚀 Запуск локально

```bash
git clone https://github.com/IgorGrigorev19/backend_store.git
cd backend_store
Создай файл .env в корне проекта и добавь в него:
PORT=3000
DB_HOST=db
DB_PORT=5432
DB_USER=postgres
DB_PASS=postgres
DB_NAME=store_db
JWT_SECRET=supersecretkey
docker compose up --build
После сборки приложение будет доступно по адресу
🌐 http://localhost:3000

Проверить работу можно запросом:

curl http://localhost:3000/health

Проверить контейнеры:

docker ps


Остановить проект:

docker compose down


Удалить контейнеры и тома:

docker compose down -v


Ожидаемый ответ:

{"status": "ok"}
