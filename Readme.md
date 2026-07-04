# DBOps Project

Учебный DBOps-проект по работе с PostgreSQL, миграциями, правами доступа и автоматизированными проверками в CI/CD.

## Назначение

Проект демонстрирует базовые практики сопровождения базы данных в инженерном процессе:

- создание отдельного пользователя для миграций и автотестов;
- настройка прав доступа в PostgreSQL;
- подготовка SQL-запросов для аналитических проверок;
- интеграция проверок в workflow.

## Используемые технологии

- PostgreSQL
- SQL
- миграции БД
- CI/CD workflow
- Shell / automation basics

## Ключевые задачи

### Пользователь для миграций

Создан отдельный пользователь `migrator`, которому выданы права, необходимые для выполнения миграций и автотестов в базе `store`.

Пример набора SQL-команд:

```sql
CREATE USER migrator WITH PASSWORD '***';
GRANT CONNECT ON DATABASE store TO migrator;
GRANT CREATE ON SCHEMA public TO migrator;
GRANT USAGE ON SCHEMA public TO migrator;
ALTER DEFAULT PRIVILEGES IN SCHEMA public
  GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO migrator;
```

### Аналитический SQL-запрос

Подготовлен запрос для расчета количества проданных товаров за предыдущую неделю:

```sql
SELECT
  o.date_created,
  SUM(op.quantity)
FROM orders AS o
JOIN order_product AS op ON o.id = op.order_id
WHERE o.status = 'shipped'
  AND o.date_created > NOW() - INTERVAL '7 DAY'
GROUP BY o.date_created;
```

## Практическая ценность

Проект релевантен для DevOps/Infrastructure задач, где требуется:

- безопасно разделять доступы к базе данных;
- понимать минимально необходимые привилегии для сервисных пользователей;
- сопровождать миграции и автотесты;
- проверять бизнес-данные SQL-запросами;
- выносить проверки в автоматизированный workflow.

## Статус

Учебный проект. Для production-использования требуется отдельная политика секретов, управление ролями через IaC/миграции и ревизия прав доступа.
