---
layout: post
title: Как установить (поднять) локальный сервер на Mac OS X Monterey на Apache2?
---
1. Сначала установим homebrew. Для этого перейдем на сайт [brew.sh](https://brew.sh/) и скопируем оттуда ссылку на установщик. После этого откроем приложение Terminal в меню приложений Mac.

2. Вставляем скопированную строку в Terminal и нажимаем Enter. Происходит установка homebrew.

3. Установим Apache2 (httpd). В Terminal пишем `brew install httpd` 

4. Создаем папку Sites. Для этого в Terminal пишем `cd ~/`, а после этого `mkdir Sites`.

5. Открываем файл настроек Apache2 (httpd) - `vim /opt/homebrew/etc/httpd/httpd.conf`.

6. Меняем порт 8080 на 80 - `Listen 80`.

7. Раскомментируем строку `#LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so`. Для этого в начале нужно удалить символ "#".

8. Находим строку DocumentRoot и значение в кавычках меняем на "/Users/имя вашего пользователя/Sites" и сразу под ним же Directory на такое же значение.

9. Прокручиваем немного вниз и меняем `AllowOverride None` на `AllowOverride All`.

10. Дальше меняем `DirectoryIndex index.html` . Добавляем перед "index.html" еще "index.php" без кавычек, чтобы была строка `DirectoryIndex index.php index.html

11. Установим php - `brew install php@7.4`. 

12. Проверяем, все ли работает правильно - пишем в терминале `echo '' > ~/Sites/index.php` и переходим на http://localhost, должна быть пустая страница.

    В следующей статье я расскажу как развернуть сайт на CMS 1C-Bitrix на локальной среде, продолжая действия выше.

