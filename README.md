# Приложение CRM-система "Ночлежка"

CRM-система для организации работы соцслужбы и приюта для бездомных (подготовлено СПбБОО "Ночлежка") 

## Шаги установки

1. Склонируйте репозиторий проекта:

    > git clone  https://github.com/code-pilots/homeless.git

2. После клонирования перейдите в каталог проекта:

    > cd homeless

3. Создайте локальные копии файлов `docker-compose.yml.dist` и `.env.dist`:
    
    > cp docker-compose.yml.dist docker-compose.yml.dist
    
    > cp .env.dist .env
    
    > cp shared/homeless/app/config/parameters.yml.dist shared/homeless/app/config/parameters.yml

    При необходимости укажите нужные настройки в этих файлах.

4. Запустите сборку контейнеров:

    > docker-compose build
    
    Если докен не установлен, то можно его установить запустив скрит исходники можно скачать с сайта https://get.docker.com/

5. После успешного окончания сборки, запустите ее:

    > docker-compose up -d

6. Подсоединитесь к symfony-приложению, запустив:
    
    > ./docker/docker/docker-symfony

7. С помощью `composer` установите необходимые библиотеки, затем укажите параметры подключения к БД:

    > composer install

8. Запустите миграцию для создания первоначальной структуры базы данных и заполнения данными: 

    > ./app/console doctrine:migrations:migrate

9. При желании можете поменять пароль для входа в систему

    > ./app/console fos:user:change-password admin

10. Сгенерируйте необходимые assets:

    > ./app/console fos:js-routing:dump

    > ./app/console assetic:dump --symlink

11. Настройте хост для проекта, перейдите по адресу хоста, 
если пароль не был изменен на шаге 9 - залогиньтесь с доступом `admin/password`.
