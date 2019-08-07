# Collections-DLE
Модуль позволит создавать подборки новостей.

Тестировался на версиях движка 13.0 и 13.2, PHP 7, MySQL 5.7 (Null)

---
 - Открытый код
 - CEO оптимизация
 - Закладки
 - Отдельная сортировка новостей
 - Добавление новости в подборки на этапе её создания
 - Разрешение на добавление группам
 - Вывод подборок в любом месте сайта
 - В админке в разделе поиск и замена так же производить замену текста в описании подборок
 - Подборки по тегам и по дополнительным полям (Если указываются теги или значения полей, очистите строку новости )
 - Быстрый поиск группы новостей по заголовку, тегам или дополнительным полям (Для каждой подборки по тегам или дополнительным полям делает запрос в базу на получение количества новостей в подборке так же не проверял работу кэша с выборкой из тегов и полей)
 - Использование с кастомным выводом новостей
 - Выводить блок в полной новости с табами по подборкам со списком новостей, или использовать определённое доп поле новости в котором будет ID подборки для вывода новостей из указанной подборки (Платно 250 рублей)
---

# Шаблоны
`login.tpl` 
  - {favorites-collections-link} - Выводит ссылку на раздел закладок подборок.

`collections_item.tpl`
  - {url} - Ссылка на подборку.
  - {title} - Выводится заголовок подборки.
    - {title limit="N"} - Выводится урезанный до N количества символов, заголовок подборки.
  - {num_elem} - Количество элементов.
  - {favorites} - Элемент добавления в закладки. (По умолчанию содержит svg объект <https://icomoon.io>)
    - Аналогичные обвёртки [add-favorites] text|img|obj [/add-favorites] и [del-favorites] text|img|obj [/del-favorites]
  - {date} - Дата обновления, формат вывода даты настраивается в настройках плагина.
    - {date=формат даты} - Выводит дату в заданном в теге формате.
  - {create_date} - Дата создания, формат вывода даты настраивается в настройках плагина.
  - {descr} - Описание.
    - {descr limit="N"} - Выводится урезанный до N количества символов, описание подборки.
  - {cover} - Обложка  
  
`shortstory_collections.tpl`
  - Все теги которые можно использовать в коротких новостях.
  
`fullstory.tpl`
  - {collections} - Выводит простые названия текстом.
  - {collections-link} - Выводит названия в виде ссылок.
  - [not-collections] text [/not-collections] - Скрывает содержимое если подборок не назначено.
  
`main.tpl` И в подключённых шаблонах.
  - {collections} - Выводит список подборок. Имеет параметры.
    - id - Выведет определённую подборку по ID. (По умолчанию выведет всё)
    - limit - Ограничить список подборок. (Если id не задан)
    - days - Указывает временной период.
    - template - Задать свой шаблон. (По умолчанию collections_block.tpl)
    - sort - Указывает порядок сортировки подборок. При использовании значения desc публикации сортируются по убыванию, а при использовании asc по возрастанию.
    - order - Критерий сортировки подборок, может принимать следующие значения:date, create_date, num_elem, name, rand. (По умолчанию date)
  - {collections ids-news id="N"} - Выводит список ID новостей принадлежащих подборке, где N id подборки. (Для использования в кастомном выводе новостей)
  - [collections-show] text [/collections-show] Выводит заключённый в теге текст на странице подборок.
  - {c-title} Выводит название подборки.
  - {c-descr} Выводит описание подборки.
    
Пример: 
 - `{collections limit="5" days="1"}` - Выведет 5 подборок которые были обновлены сегодня.
 
 Теги используемые в шаблонах тега `{collections}` (По умолчанию: **collections_block.tpl**)
 - {url} - Ссылка на подборку.
 - {title} - Выводится заголовок подборки.
    - {title limit="N"} - Выводится урезанный до N количества символов, заголовок подборки.
 - {num_elem} - Количество элементов.
 - {cover} - Обложка.
 - {date} - Дата обновления, формат вывода даты настраивается в настройках плагина.
    

# ЧПУ
В файле `.htaccess` Добавить ниже строки `RewriteEngine On`
```
RewriteRule ^collections/([0-9]+)-(.*)/page/([0-9]+)(/?)+$ index.php?do=collections&id=$1&cstart=$3 [L]
RewriteRule ^collections/([0-9]+)-(.*)(/?)+$ index.php?do=collections&id=$1 [L]
RewriteRule ^collections/favorites(/?)+$ index.php?do=collections&action=favorites [L]
RewriteRule ^collections/favorites/page/([0-9]+)(/?)+$ index.php?do=collections&action=favorites&cstart=$1 [L]
RewriteRule ^collections/page/([0-9]+)(/?)+$ index.php?do=collections&cstart=$1 [L]
RewriteRule ^collections(/?)$ index.php?do=collections [L]
```
# Скриншоты

<p>
<img src="https://user-images.githubusercontent.com/44625352/55650636-9ecf6f80-57e6-11e9-86e1-cff1eec8b3fa.png" width="430">
<img src="https://user-images.githubusercontent.com/44625352/62590580-875bdc80-b8d5-11e9-8cb8-8a4fc97777b3.jpg" width="430">
<img src="https://user-images.githubusercontent.com/44625352/55650754-e0f8b100-57e6-11e9-92fa-8d9d176dbb2f.png" width="430">
<img src="https://user-images.githubusercontent.com/44625352/55650753-e0601a80-57e6-11e9-981f-2877fb2cadf8.png" width="430">
<img src="https://user-images.githubusercontent.com/44625352/55650756-e0f8b100-57e6-11e9-9a94-12bf6a018785.png" width="430">
<img src="https://user-images.githubusercontent.com/44625352/55650574-6039b500-57e6-11e9-83e6-daaff65c6129.png" width="430">
</p>

# Скриншоты дополнения блоков в полной новости
<p>
<img src="https://user-images.githubusercontent.com/44625352/62590379-ce959d80-b8d4-11e9-9d15-fcaec7633050.jpg" width="430">
<img src="https://user-images.githubusercontent.com/44625352/62590380-ce959d80-b8d4-11e9-8e8e-05e271592bcc.jpg" width="430">
</p>

### Donate
Для материальной благодарности.

<img src="https://qiwi.com/favicon.ico" width="16" height="16"> [Qiwi](https://qiwi.me/teramoune)

<img src="https://www.webmoney.ru/img/logo-wm-sat-small.png" width="139" height="34">

 - R425445633105
 - Z990082286464
 
teramoune@gmail.com
Telegram: @TeraMoune
