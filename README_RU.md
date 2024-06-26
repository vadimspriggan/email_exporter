
# Email Exporter
![Project Cover](./image.png)

Эта программа создана для быстрого и легкого извлечения всех писем или выбранных папок с любого почтового сервера, который поддерживает IMAP. Программа поддерживает выгрузку с неограниченного количества почтовых ящиков, указанных в конфигурационном файле.

## Особенности

- Поддержка IMAP-серверов.
- Возможность выбрать конкретные папки для выгрузки.
- Проверка выгрузки с помощью контрольных сумм.
- Опция удаления выгруженных писем с сервера.
- Выгрузка всех писем с вложениями или только вложений.
- Удобный конфигуратор для управления конфигурационным файлом.

## Установка

1. Склонируйте репозиторий:
    ```bash
    git clone <URL>
    ```

2. Перейдите в директорию проекта:
    ```bash
    cd mailexport
    ```

3. Установите необходимые зависимости:
    ```bash
    pip install -r requirements.txt
    ```

## Использование

### Конфигуратор

Для настройки конфигурационного файла используйте `make_config.py`.

#### Запуск конфигуратора
```bash
python make_config.py
```

### Основная программа

Для запуска основной программы используйте `main.py`.

#### Запуск основной программы
```bash
python main.py
```

### Описание работы

При запуске `main.py` программа сначала проверяет количество серверов в конфигурационном файле и предлагает изменить его, если это необходимо. 

```plaintext
Сейчас в конфигурационном файле n серверов
Хотите изменить конфигурационный файл? (y/N)
```

Если пользователь выбирает `y`, запускается `make_config.py` для редактирования конфигурации. После завершения работы конфигуратора программа продолжает работу с обновленной конфигурацией.

#### Опции сохранения

Программа предлагает выбрать опцию сохранения:
1. Сохранение только `.eml` файлов.
2. Сохранение только вложений.
3. Сохранение и `.eml` файлов, и вложений.

#### Путь для сохранения

Пользователь может указать полный путь для сохранения выгрузки. Если путь не указан, папки будут созданы на уровень выше текущей директории.

#### Проверка выгрузки

По умолчанию, включена проверка выгрузки, которая выполняется с помощью контрольных сумм. Для каждого письма вычисляется контрольная сумма MD5, которая затем проверяется после сохранения письма. Если контрольная сумма не совпадает, письмо скачивается заново до трех раз.

#### Удаление проверенных писем

Если проверка включена и выбрана опция 1 или 3, пользователю предлагается возможность удаления проверенных писем с сервера.

### Примеры

#### Пример конфигурационного файла (`config.json`)

```json
{
    "accounts": [
        {
            "IMAP_SERVER": "imap.gmail.com",
            "EMAIL_ACCOUNT": "your_email@gmail.com",
            "EMAIL_PASSWORD": "your_password"
        },
        {
            "IMAP_SERVER": "imap.yandex.com",
            "EMAIL_ACCOUNT": "another_email@yandex.com",
            "EMAIL_PASSWORD": "another_password"
        }
    ]
}
```

### Структура проекта

- `main.py`: Основной скрипт для запуска выгрузки писем.
- `make_config.py`: Конфигуратор для управления конфигурационным файлом.
- `config.py`: Модуль для загрузки и сохранения конфигурационного файла.
- `imap_handler.py`: Модуль для работы с IMAP-серверами.
- `utils.py`: Вспомогательные функции для обработки писем и вложений.
- `config.json`: Конфигурационный файл с учетными записями почтовых серверов.

### Лицензия

Этот проект лицензирован на условиях GPL-3.0 License.
