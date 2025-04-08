# dbops-project
Исходный репозиторий для выполнения проекта дисциплины "DBOps"

**Шаг 2. Создайте ещё одну БД в PostgreSQL, допустим, это будет база store.** 
 1) psql "host=localhost port=5432 dbname=store_default user=user"
 2) CREATE DATABASE store;
**Шаг 3. Создайте нового пользователя PostgreSQL и выдайте ему права на все таблицы в базе store. Под этим логином будут ходить автотесты и выполняться миграции, поэтому важно выдать достаточные для этой работы права. Укажите выполненные для этого запросы в файле репозитория Readme.md.**
1)CREATE USER migrator WITH PASSWORD 'password';
2)GRANT CONNECT ON DATABASE store TO migrator;
3)GRANT USAGE ON SCHEMA public TO migrator
4)ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO migrator;  
**Шаг 4. В репозитории в директории migrations создайте файл V001__create_tables.sql и опишите в нём DDL-запросы на создание таблиц. Получившиеся запросы должны повторять структуру, которая есть у существующей БД, заполненной в результате работы скрипта.**


**Шаг 5. Добавьте в workflow-файл шаг, в котором будет запускаться миграция Flyway к созданной вами БД store. Не забудьте добавить чувствительные переменные, такие как DB_HOST, DB_PORT, DB_USER, DB_PASSWORD, в секреты GitHub.**



**Шаг 6. Сделайте коммит и пуш в репозиторий. В результате выполнения пайплайна в БД store появится описанная вами структура таблиц, а автотесты должны зафиксировать прохождение тестов TestTask1/*:**
**
