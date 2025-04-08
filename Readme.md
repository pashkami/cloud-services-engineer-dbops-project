# dbops-project
Исходный репозиторий для выполнения проекта дисциплины "DBOps"

**Создайте нового пользователя PostgreSQL и выдайте ему права на все таблицы в базе store. Под этим логином будут ходить автотесты и выполняться миграции, поэтому важно выдать достаточные для этой работы права. Укажите выполненные для этого запросы в файле репозитория Readme.md.**


1)CREATE USER migrator WITH PASSWORD '****';
2)GRANT CONNECT ON DATABASE store TO migrator;
3)GRANT CREATE ON SCHEMA public TO migrator;
3)GRANT USAGE ON SCHEMA public TO migrator
4)ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO migrator;  

**Какое количество сосисок было продано за предыдущую неделю**
Также добавил вывод в workflow
SELECT o.date_created, SUM(op.quantity) 
         FROM orders AS o JOIN order_product AS op ON o.id = op.order_id 
         WHERE o.status = 'shipped' AND o.date_created > NOW() - INTERVAL '7 DAY' GROUP BY o.date_created;
