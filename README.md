# Task Manager API

REST API built with **Symfony + API Platform + Docker** for task management.

## Prerequisites
- Docker & Docker Compose
- VSCode
- Composer (global)
- Symfony CLI (optional)
- Postman (desktop)

## 1. Create Project Folder
## 2. Create Symfony Project
- symfony new (project_name) --webapp --version=lts

## 3. Docker Setup
- Create docker-compose.yaml
- Congigure environment
    - edit .env file
- Start services
    - docker:build
    - symfony docker:up -d
    - symfony docker:exec app composer install

## 4. API Platform Setup
- symfony composer require "api-platform/core:^3.3" -W
- symfony composer require orm maker --dev

## 5. Create Task Entity
- symfony console make:entity Task

## 6. Add API Groups 
- Edit src/Entity/Task.php
    - Add #[Groups(['task:read', 'task:write'])] to all fields

## 7. Generate API & Migrate
- symfony console make:crud Task --api-resource
- symfony console make:migration
- symfony console doctrine:migrations:migrate

## 8. Configure API Routes
- code config/routes.yaml
    - api_platform:
        resource: .
        type: api_platform
        prefix: /api

## 9. Finalize
- symfony console cache:clear
- symfony server:start

## 10. Test API
- http://localhost:8000/api/docs     # Swagger UI
- http://localhost:8000/api/tasks    # JSON data
