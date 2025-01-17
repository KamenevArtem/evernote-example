# evernote-exaample

Программа представляет собой набор скриптов, позволяющих взаимодействовать с API Evernote для создания, хранения и вывода заметок:

* `add_note2journal.py` - позволяет создать и сохранить запись в указанный блокнот;
* `config.py` - опредеяет класс для зваимодействия с переменными окружения;
* `dumb_inbox.py` - позволяет вывести в консоль список заметок из конкретного блокнота;
* `list_notebooks.py` - выводит список всех имеющихся блокнотов.

## Как установить

Для полноценного функционирования программы необходимо создать файл `.env`, содержащий следующий переменные в формате "Насзвание"="Значение":

* `EVERNOTE_PERSONAL_TOKEN` - токен, необходимы для работы с API. Может быть получен на [сайте](https://dev.evernote.com/doc/articles/dev_tokens.php), пройдя инструкцию. Однако, в настоящее время получить токен на сайте невозможноя, необходимо обратиться к службе поддержки;
* `JOURNAL_TEMPLATE_NOTE_GUID` - GUID заметки, которая будет использоваться как шаблон для создания других заметок;
* `JOURNAL_NOTEBOOK_GUID` -  GUID блокнота, который будет использоваться для записи новых заметках по шаблону;
* `INBOX_NOTEBOOK_GUID` - GUID блокнота, из которого выводятся заметки.

При корректном выполнении описанных выше шагов, скрипт считает переменные окружения и запустится. Python3 должен быть уже установлен. Затем используйте pip (или pip3, есть конфликт с Python2) для установки зависимостей:

```
pip install -r requirements.txt
```

## Как запустить

Пользователь имеет возможность исользовать 3 функции, вызывая один из скриптов:

### list_notebooks.py

Выводит список имеющихся блокнотов. Запускается через консоль командой:

```python
python list_notebooks.py
```

Скрипт после запроса к API выведит список в формате: GUID "Название блокнота"

### bump_inbox.py

Выводит список заметок из конкретного блокнота.
Чтобы он функционировал, необходимо, чтобы у пользователя уже имелся блокнот Evernote с киким-то набором записей. Для создания блокнота:
* перейдите на [сайт Evernote](https://evernote.com/intl/ru);
* создайте блокнот и любые записи в нем;
* запустите `list_notebooks.py` для получения GUID блокнота, который необходимо ввести в переменную `INBOX_NOTEBOOK_GUID` файла .env

После этого, через консоль можно запустить скрипт командой:

```
python dump_inbox.py
```

По умолчанию скрипт выводит 10 последних заметок. Но при запуске можно передать ему в качестве первого параметра командной строки число - максимальное количество выводимых заметок.

### add_note2journal.py

Скрипт позволяет внести в блоктон новую запись, соответствующую шаблону. Для того работы с ним необходимо, чтобы на сайте Evernote имелась заметка, которую скрипт будет использовать в качестве шаблона, блокнот в который будут вноситься заметки. При выполнении описанных выше шагов, необходимо сделать следующее в имеющемся блокноте:

* создать заметку с заголовком: "Заметка {date} {dow} # шаблон"
* запустить dumb_inbox.py
* записать в выведенный в консоль GUID заметки, который скрипт будет воспринимать в качестве GUID шаблона, в переменную JOURNAL_TEMPLATE_NOTE_GUI файла .env

Запускается при помощи консоли командой:

```python
python add_note2journal.py
```

Будет внесена новая заметка с текущей датой. Также пользователю в консоле будет выведенно сообщение об успешном создании заметки. Есть возможность в качестве параметра в консоли передать желаемую дату заметки в формате `YYYY-MM-DD`.

## Цель проекта

Код написан в образовательных целях на онлайн-курсе для веб-разработчиков [devman](https://devman.org/)

