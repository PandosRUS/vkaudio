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
            hash: "Хэш аудио, передается при скачивании"
        },
        {
            ...
        }
    ]
]
```
## Сохранение аудио на сервер
GET запрос:
```
/API.php?method=load&type=response&hash=`хэш_аудио`
```
> В данном запросе страница будет прогружаться до полного
> скачивания аудиозаписи на сервер и вернет её url  

Ответ
```js
[
    'http://example.com/audio/temp.mp3'
]
```
***
