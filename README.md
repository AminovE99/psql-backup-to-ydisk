# POSTGRESQL BACKUP TO YANDEX DISK

Утилита для создания, сохранения и восстановления резервных копий из базы данных postgresql. Хранилище Yandex Disk

В установленные сроки по cron заданию выполняется бэкап базы данных. Затем этот бэкап загружается в Yandex Disk. В диске резервные копии находятся в папке Приложения/имя-вашего-проекта (`https://disk.yandex.ru`). Копии разделены по месяцам чтобы удобно было ориентироватся. Если кое где будет ошибка будет отправлен отчет в указанную почту.

## Получение токена доступа
1. Региструем свое приложение в yandex `https://oauth.yandex.ru/client/new`. Выбираем Яндекс.Диск REST API и права: Доступ к информации о диске, Доступ к папке приложения на диске. Сохраняем полученные данные.
2. Заходим по этой ссылке `https://oauth.yandex.ru/authorize?response_type=token&client_id=<client_id>` и получаем токен доступа. Токен действует 1 год.
3. Полученный YANDEX_DISK_ACCESS_TOKEN & YANDEX_DISK_APP_FOLDER записываем в конфигурацию.

## Пример конфигурации docker-compose.yml
Смотри файл docker-compose.example.yml

## Бэкап по требованию

1. Войти в контейнер `docker exec -it <container_id> <db_name>`
2. Запустить бэкап `./app backup`

## Восстановление из бэкапа
1. Войти в контейнер `docker exec -it <container_id> <db_name>`
2. Запустить процесс восстановления `./app restore <folder>/<file> <db_name>`. Путь файла на ydisk - `<folder>/<file>`
