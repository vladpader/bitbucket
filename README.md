# README

## Запуск основного приложения

Перейти в корень проекта и выполнить

```shell
cd Api
docker compose down
docker compose up -d --build
```

## Накатка миграций

Перейти в корень проекта и выполнить

```shell
cd Api
dotnet ef database update 
```

При первом запуске будет ошибка - это нормально.

## Создание администратора

```shell
curl -X POST "http://localhost:5201/api/admin/create-admin" -H "apiKey: supersecretkey"
```

## Документация на API

Открыть [http://localhost:5201/swagger/index.html](http://localhost:5201/swagger/index.html).

## Ручной запуск парсера логов

```shell
curl -X POST http://localhost:5201/api/logs/parser/parse
```

Также, парсер логов запускается по крону при старте докер-образа.

## UI приложения

[http://localhost:5201/](http://localhost:5201/)

### Вход под администратором

Имя пользователя: `admin`
Пароль: `Admin123!`

## Запуск консольного приложения

Перейти в корень проекта и выполнить

```shell
cd LogConsoleApp
dotnet build
dotnet run
```

## Запуск тестов

Перейти в корень проекта и выполнить

```shell
cd MyWebApiProject.Tests
dotnet test
```

В результате могут быть незначительные предупреждения, но все тесты проходят успешно.

## Отладка API через CURL

Полезные команды

```shell
# Остановить приложение
docker compose down

# Удалить образы приложения (очистка данных)
docker compose down --volumes

# Просмотр логов API-приложения
docker logs my_webapi

# Залогиниться под админом
curl -X POST "http://localhost:5201/api/auth/login" -H "Content-Type: application/json" -d '{"userName": "admin", "password": "Admin123!"}' -c cookies.txt

# Посмотреть список пользователей
curl -X GET "http://localhost:5201/api/user" -b cookies.txt

# Добавить нового пользователя
curl -X POST "http://localhost:5201/api/auth/register" -H "Content-Type: application/json" -d '{"userName": "test", "email": "test@test.com", "password": "Admin123!"}'

# Отладка WebSocket
wscat -c "ws://localhost:5201/ws/chat?userId=<userId>"
```
