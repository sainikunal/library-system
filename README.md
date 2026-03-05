# 📚 Library System

Welcome to the **Library System**! This project is a comprehensive application built with **Python**, **Django**, **Django REST Framework (DRF)**, and **Celery**. It manages authors, books, members, and loans within a library context. The application is fully containerized using **Docker**, allowing for easy setup and deployment.

---

## 📌 **Project Overview**
This application enables **library management** by allowing users to manage authors, books, members, and loans efficiently.

### **Tech Stack**
- **Python 3.9** – Backend development.
- **Django 4.2** – Web framework.
- **Django REST Framework** – API development.
- **Celery 5.3** – Task queue for async jobs.
- **Redis 6** – Message broker for Celery.
- **PostgreSQL 13** – Database.
- **Docker & Docker Compose** – Containerized setup.

---

## 🛠 **Setup Instructions**

### 1️⃣ **Clone the Repository**
```sh
git clone https://github.com/sainikunal/library-system.git
cd library-system
```

### 2️⃣ **Create a `.env` File**
Create a `.env` file in the root directory to store environment variables:
```sh
touch .env
```

#### 📌 **Content of `.env`**
```env
DEBUG=1
DJANGO_ALLOWED_HOSTS=localhost 127.0.0.1 [::1]
DATABASE_URL=postgres://library_user:library_password@db:5432/library_db
CELERY_BROKER_URL=redis://redis:6379/0
CELERY_RESULT_BACKEND=redis://redis:6379/0
SECRET_KEY=your-secret-key
DEFAULT_FROM_EMAIL=admin@library.com
```
> **Note:** Replace `your-secret-key` with a secure key. Ensure that `.env` is included in `.gitignore`.

### 3️⃣ **Build and Run Docker Containers**
```sh
docker-compose build
docker-compose up
```
This command will:
- Start PostgreSQL (`db`) and Redis (`redis`) services.
- Build and run the Django application (`web`).
- Run the Celery worker (`celery`).

### 4️⃣ **Initialize the Django Project**
Apply migrations and create a superuser:
```sh
docker-compose run web python manage.py makemigrations
docker-compose run web python manage.py migrate
docker-compose run web python manage.py createsuperuser
```
Follow the prompts to create a superuser account.

### 5️⃣ **Start the Application**
```sh
docker-compose up
```
To stop the running containers, press `CTRL+C` in the terminal where `docker-compose up` is running, then execute:
```sh
docker-compose down
```

---

## 📂 **Project Structure**
```plaintext
library-system/
├── docker-compose.yml
├── Dockerfile
├── requirements.txt
├── .env
├── .gitignore
├── manage.py
├── library_system/
│   ├── __init__.py
│   ├── asgi.py
│   ├── celery.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── library/
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── serializers.py
    ├── tasks.py
    ├── tests.py
    └── views.py
```

---

## 📌 **Accessing the Application**

### 🔑 **Django Admin Interface**
- **URL:** [http://localhost:8000/admin/](http://localhost:8000/admin/)
- **Login:** Use the superuser credentials you created.
- **Functionality:** Manage authors, books, members, and loans through the admin panel.

### 📌 **API Endpoints**
| Method | Endpoint          | Description |
|--------|------------------|-------------|
| `GET`  | `/api/authors/`  | Fetch all authors |
| `GET`  | `/api/books/`    | Fetch all books |
| `GET`  | `/api/members/`  | Fetch all members |
| `GET`  | `/api/loans/`    | Fetch all loans |
| `POST` | `/api/authors/`  | Create a new author |
| `POST` | `/api/books/`    | Create a new book |
| `POST` | `/api/members/`  | Create a new member |
| `POST` | `/api/loans/`    | Create a new loan |

---

## 🎯 **License**
This project is licensed under the **MIT License**.

---

🚀 **Happy coding!** 🎉