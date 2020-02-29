# vkaudio
## Необходимая структура
```css
public_html
├── audio // Директория для скачанных аудиозаписей
├── cache
│   └── cookies.txt // Кеш авторизаций
├── classes
│   ├── AuthVK.php
│   ├── GetUrlAudio.php
│   ├── LoadAudio.php
│   ├── PostVK.php
│   └── SearchAudios.php
├── API.php
└── config.php
```
## Поиск в общем списке
GET запрос:
```
/API.php?method=search&text=`поисковой_запрос`
```
Ответ
```js
[
    'success',
    [
        {
            artist: "Исполнитель",
            name: "Название",
            img_min: "URL изображения 80х80",
            img: "URL изображения 150х150",
            hash: "Хеш аудио, передается при скачивании"
        },
        {
            ...
        }
    ]
]
```
> За один запрос ВК возвращает не более 100 аудиозаписей, получение следующей страницы пока что не предусмотрено

Типы ошибок:

    'enter_query' - не введен поисковой запрос
## Сохранение аудио на сервер
GET запрос:
```
/API.php?method=load&type=response&hash=`хеш_аудио`
```
> В данном запросе страница будет прогружаться до полного
> скачивания аудиозаписи на сервер и в конце вернет её url  

Ответ
```js
[
    'http://example.com/audio/temp.mp3'
]
```
***
GET запрос:
```
/API.php?method=load&type=no_response&hash=`хеш_аудио`
```
> В данном запросе сервер сразу вернет ответ о том, что
> началось скачивание аудиозаписи до окончания скачивания, очевидно, страница не будет грузиться более 0.1 сек,
> что предотвратит долгое ожидание ответа от curl`а
> 
> Для проверки статуса скачивания аудио необходимо использовать следующий API с этим же хешем

Ответ
```js
[
    'start'
]
```
***
GET запрос:
```
/API.php?method=load&type=check&hash=`хеш_аудио`
```
> Cтатус скачивания аудио

Ответ
```js
[
    'no_found'
]
```
```js
[
    'waiting'
]
```
```js
[
    'ready',
    'http://example.com/audio/temp.mp3'
]
```
