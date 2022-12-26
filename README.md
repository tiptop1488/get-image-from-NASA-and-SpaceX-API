# Сбор и публикация в телеграм канал фотографии космоса и запуска ракет

Набор скриптов предназначен для скачивания и последующей отправки в телеграм канал: 
* фотографий космоса и земли, сделанных NASA 
* фотографий с запуска ракет SpaceX

## Установка

Для запуска потребуется `python 3` и библиотеки перечисленные в файле `requirements.txt`. Для установки используйте команду:

```
pip install -r requirements.txt
```

Все файлы запускаются по отдельности, кроме `additional_scripts.py`, в нем хранятся вспомогательные скрипты.
Все скачанные фотографии сохраняются в в директорию `images`. Если данной директории нет в проекте - она создасться автоматически.
Так же вам потребуется создать файл `.env` и добавит переменные окружения.

```
NASA_API_KEY = 'ваш ключ API для работы с NASA'
TELEGRAM_TOKEN = 'токен вашего телеграм бота'
TG_CHAT_ID = 'id канала для публикаций'
```

## fetch_nasa_apod_images.py

Скачивает в директорию `images` 30 фотографии космоса от NASA серии APOD. Аргументов на вход не принимает.

```
python3 fetch_nasa_apod_images.py
```

## fetch_nasa_epic_images.py

Скачивает в директорию `images` фотографии земли от NASA серии EPIC. Аргументов на вход не принимает.

```
python3 fetch_nasa_epic_images.py
```

## fetch_spacex_images.py

Скачивает в директорию `images` фотографии с запуска ракет SpaceX. Принимает на вход один необязательный аргумент - id запуска. Если id не указан, скачает фотографии последнего запуска. Если на последнем запуске фотографии не делались, скачает фотографии запуска-примера.

```
python3 fetch_spacex_images.py --launch_id 5eb87d47ffd86e000604b38a
```

## telegram_sender_bot.py

Отправляет фотографию в телеграм канал. На вход принимает один необязательный элемент - название фотографии.
Если фотографи не найдена или аргумент не указан опубликует рандомную фотографию из тех что есть в директории `images`.

```
python3 telegram_sender_bot.py --name_photo NASA_8.jpg
```

## telegram_endless_sender_bot.py

По очереди отправляет фотографии из директории `images` в телеграм канал. Если отправленны все фотографии, продолжает публиковать снимки в рандомном порядке.
На вход принимает один необязательный элемент - время между публикациями. Время указывается в часах. Если аргумент не передан, стандарнтная задержка между публикациями составляет 4 часа.

```
python3 telegram_endless_sender_bot.py --time_slip 1
```

## additional_scripts.py

Набор функций для работы с API spaceX и NASA которые использются в описанных ранее скриптах.
