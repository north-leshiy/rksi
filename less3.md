# Знакомство со структурой
Первое приближение.

app - папка с основным кодом приложения.
В ней обычно описывается вся логика.

config - папка с конфигурацией системы

.env файл - конфигурация, зависимая от площадки окружения

database с сидерами и миграциями - для наполнения и миграций БД. Разберем позже.

resources/views - шаблоны
resources/lang - языковые переводы
resources/assets - статика


# Знакомства c роутами

1. перейти на страницу и увидеть 404
2. Примитивный роут

    ```
    Route::get('/', function(){
        return 'hello world!';
    });
    ```

3. Роут + view

    ```
    Route::get('/hello', function(){
        return view('hello');
    });
    ```
    
    + создаем в папке resources/views
    файл hello.blade.php
    
    В нем пишем примитивный html
    
    ```
       <!doctype html>
       <html lang="en">
       <head>
           <meta charset="UTF-8">
           <title>TEST VIEW</title>
       </head>
       <body>
            <h1>Hello test view</h1>
       </body>
       </html>
    ```
    
    Открываем страницу, должны увидить свою вьюху

4. Передача параметров в route

    ```
    Route::get('/test', function(){
        return view('hello')->with('name', 'John');
    });
    ```
    
    Изменяем вывод шаблона 
    <h1>Hello <?=$name?></h1>
    
    Проверяем
    
    Пвторяем тоже самое с blade синтаксисом
    <h1>Hello {{$name}}</h1>
    
5. Передача массива в параметры

    ```
    Route::get('/hello', function(){
        $arTasks = [
            'task one',
            'task two',
            'task three'
        ];
        return view('hello', compact('arTasks'));
    });
    
    ```
    
    
    php sintax
    
    ```
    <ul>
        <?php foreach ($arTasks as $task): ?>
        <li><?=$task?></li>
        <?php endforeach; ?>
    </ul>
    ```
    
    blade sintax
    
    ```
    <ul>
        <?php foreach ($arTasks as $task): ?>
        <li><?=$task?></li>
        <?php endforeach; ?>
    </ul>
    ```
6. просмтотр списка роутов через терминал
Выведем все текущие роуты которые мы назначили.

```
php artisan route:list
```

7. Контроллеры

Контроллеры представляют собой отдельные классы, которые управляют логикой запросов вашего приложения

Создадим контроллер через консольную команду artisan, находясь в папке private
```php artisan make:controller HomeController```

В директории app/Http/Controllers/ должен был создастся новый файл-болванка контроллера.

Напишем в нем метод index(), который подключи view('hello').

Перенаправим наш роут в контроллер
```
Route::get('/hello', [
    'uses' => 'HomeController@index',
    'as' => 'hello'
]);
```

Где uses - это имя контролера@имя метода.
as - имя роута, которое пригодится потом для использования ссылки.
