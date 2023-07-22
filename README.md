# replication_db
### Репликация и резервное копирование

Домашнее задание к занятию «Репликация и резервное копирование»
Цель задания
Выполнив это задание, вы:

Научитесь работать с WAL-логами.
Попрактикуетесь в настройке механизма логической репликации.
Поработаете с процедурами резервного копирования.
Чеклист готовности к домашнему заданию
Есть ранее созданная БД PostgreSQL для выполнения заданий.
Пререквизиты
Поднять второй экземпляр PostgreSQL с новой БД — «test2» для выполнения задач по репликации.

Для этого:

Создайте второй экземпляр, выполните команду: /usr/lib/postgresql/15/bin/initdb -D /var/lib/postgresql/15_2/main.

Для работы экземпляра требуется сменить порт работы с дефолтного 5432, на котором работает 1-ый экземпляр, на порт 5433, на котором будет работать 2-ой экземпляр. Выполните команду: vi /var/lib/postgresql/15_2/main/postgresql.conf, где /var/lib/postgresql/15_2/main/postgresql.conf является файлом конфигурации 2-го экземпляра PostgreSQL.

Запустите второй экземпляр. Выполните команду: /usr/lib/postgresql/15/bin/pg_ctl -D /var/lib/postgresql/15_2/main start.

Если потребуется перезапустить 2-ой экземпляр, выполните команду: /usr/lib/postgresql/15/bin/pg_ctl -D /var/lib/postgresql/15_2/main restart.

**Задание 1**

Проверьте текущую роль сервера, определите текущий сгенерированный WAL-лог, выполнив команду в соответствии с ролью сервера. Покажите, что на файловой системе этот последний лог является свежим изменяемым логом: используйте команду shell 'ls'.
![01](https://github.com/INRI03/replication_db/blob/main/001.png)

Сделайте дамп таблицы tab1 с данными в тестовой БД test и импортируйте его в БД test2.
Удалите все данные из импортированной таблицы tab1, с которой работали в пункте 2 этого задания, в БД test2 и настройте репликацию для неё в БД test2 из БД test с репликаций операций только update. Убедитесь, что репликация работает при выполнении апдейтов в БД test и что операции insert не реплицируются.
![01](https://github.com/INRI03/replication_db/blob/main/002.png)
![01](https://github.com/INRI03/replication_db/blob/main/003.png)
![01](https://github.com/INRI03/replication_db/blob/main/004.png)

**Задание 2**

Определите текущий сгенерированный WAL-лог на сервере, а затем выполните команду переключения WAL-лога. Подтвердите, что он переключился: номер лога изменился.
![01](https://github.com/INRI03/replication_db/blob/main/005.png)

Сделайте дамп таблицы tab1 в тестовой БД test и импортируйте его в БД test2 без данных, то есть таблица в БД test2 должна быть пустой.
Настройте репликацию для БД test2 из БД test для таблицы tab1, с которой работали в пункте 2 этого задания, с репликацией только insert и update операций. Убедитесь, что репликация работает:
при выполнении любых операций в БД test;
в БД test2 реплицируются только операции insert и update;
не попадают другие операции, например delete.
![01](https://github.com/INRI03/replication_db/blob/main/006.png)
![01](https://github.com/INRI03/replication_db/blob/main/007.png)
![01](https://github.com/INRI03/replication_db/blob/main/008.png)
