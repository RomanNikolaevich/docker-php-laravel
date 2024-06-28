## Збірка Docker для запуску Laravel

## Запуск проекта:
1. Скопіювати цей код в проект з Laravel, папку `public` для Laravel переносити не потрібно
2. В файлі `.env`:
   * `DB_HOST=127.0.0.1` міняємо на `DB_HOST=db` (Database Service)
   * Додаємо `DB_ROOT_PASSWORD=root` (за замовчуванням користувач root та пароля немає) 
   * Додаємо данні про свого користувача БД та пароль: `DB_USERNAME` та `DB_PASSWORD`
   * Далі потрібно саме в БД створити нового користувача та додати йому потрібних доступів та повноважень - ці данні 
   потрібні співпадати з  `DB_USERNAME` та `DB_PASSWORD` (без цього міграція буде видавати помилку)
3. Для виконання міграції перейти в контейнер з php та виконати міграцію:
   * `docker exec -it project-php bash`
   * `php artisan migrate`
4. Якщо потрібна інша версія PHP, то можна вибрати для цієї версії Dockerfile [тут](https://github.com/docker-library/docs/blob/master/php/README.md#supported-tags-and-respective-dockerfile-links)
5. Якщо не потрібен `xDebug`, то треба закоментувати, змінити або видалити ці поля в `php.ini` та `Dockerfile`

## Docker - основні команди:

* Збірка образів

  `docker-compose build`

* Запуск контейнерів у фоновому режимі

  `docker-compose up -d`

* Зупинка та видалення контейнерів:

  `docker-compose down`

* Зупинка та видалення контейнерів та томів:

  `docker-compose down -v`

* Збірка образів та запуск контейнерів у фоновому режимі

  `docker-compose up --build -d`

## Docker - работа у терміналі:

* зайти в контейнер ("nginx" - це назва контейнеру):

    `docker exec -it nginx bash`

* відобразити всі файли та папки у вигляді списку:

    `ls -la`

* зайти в папку etc:

    `cd etc`

* відобразити в терміналі шлях до папки (корисно, щоб скопіювати та не набирати)

    `pwd`

* вихід з контейнера:

    `exit`



## Помилки:
* Якщо виникає помилка "Failed to open stream: Permission denied":

  `sudo chgrp -R www-data storage bootstrap/cache`

  `sudo chmod -R ug+rwx storage bootstrap/cache`


* Якщо виникає помилка, що потрібно згенерувати ключ:

    `php artisan key:generate`


