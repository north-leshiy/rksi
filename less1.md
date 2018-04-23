# Подключене по SSH через winscp

Доступы - в таблицы. 
Сам процесс не описывается, легко гуглится.
Подключаем к winscp PUTTY клиент.

# Установка laravel
Работа через putty/ssh терминал.

Справочно
- https://laravel.com/docs/5.6 - установка laravel

1. Переходим в директорию домена 

    ```cd ~/web/ip.rksi.w6p.ru/private/```
    
    где 
    - ip.rksi.w6p.ru - название вашего домена.
    - ~ - символ домашней директории пользователя

2. Устанавливаем глобально для вашего пользвоателя laravel установщик
```composer global require "laravel/installer"```

3. устанавливаем laravel в текущую папку (символ точки в конце)
composer create-project --prefer-dist laravel/laravel .

4. СимЛинк и DOCUMENT_ROOT

Справочно:
- https://ru.wikipedia.org/wiki/Символическая_ссылка
- Директория которую веб сервер ассоциирует с корнем веб-домена называют DOC_ROOT


По умолчанию DOCUMENT_ROOT веб-севрер ссылается на `~/web/ip.rksi.w6p.ru/public_html/`.

Нам необходимо чтобы DOC_ROOT ссылался на `~/web/ip.rksi.w6p.ru/private/public/`
    

Удаляем public_html и делаем симлинк.

```
cd ../
rm -r publick_html
ln -s private/public public_html
```

После этого у вас при открытии в браузере вашего домена должна появиться приветственная страница laravel (выглядит примерно так).

![Laravel](https://w6p.ru/MjhkN2.png)
