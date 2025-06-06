# Поиск и исправление ошибок текста

При работе с проектом теперь есть возможность проверить наличие ошибок в полуавтоматическом режиме.

## Поиск ошибок в личной статье

Если вы хотите проверить вашу статью на наличие ошибок выполните эти действия:

1. Скопируйте локальный путь до файла статьи

![path-copy](/reference/test/speller/path-copy.png)

2. Выполните команду:

```shell
npm run docs:speller {Путь из шага 1}
```

И после этого перед вашими глазами будут все ошибки в вашей статье, а также возможные варианты исправления.

![speller-result](/reference/test/speller/speller-result.png)

## Глобальный поиск для редакторов

Для вас существует отдельная команда, которая проверяет все файлы проекта

```shell
npm run docs:speller-full
```

После проверки, в случае использования VSCode, вы можете быстро переходить к файлам нажимая по их названиям используя [[Ctrl]] + [[🖱️ Left Click]]

## Исправление ошибок

Посмотрим на вывод команды:

![speller-result](/reference/test/speller/speller-result.png)

```text
2. наличее (3:57, count 2, suggest: наличие)
      |     |  |    |          |______________ Возможный вариант исправления
      |     |  |    |_________________________ Количество повторений ошибки
      |     |  |______________________________ Номер символа начала слова в строке
      |     |_________________________________ Номер строки в котором допущена ошибка
      |_______________________________________ Слово в котором допущена ошибка
```

Для начала все просто - исправляйте все орфографические ошибки и опечатки, которые найдёт команда.

Но в процессе изменений могут возникнуть проблемы. И для этого есть возможность внести свои изменения в словарь.

## Дополнение словаря

Для дополнения словаря нужно открыть файл `.yaspellerrc` и добавить слово с новой строки в разделе `"dictionary"`

::: warning В каком случае стоит добавлять слово в словарь?

- Название ПО или любых других имён, в правильности написания которого вы полностью уверены

  `(Например: Flatseal, ALT Gnome)`

- Технический термин или локализированное заимствование

  `(Например: WiFi, тикет, форк, коммит)`

- Нетипичные использования слов, при цитировании элементов интерфейса, которые не может распознать программа

  `(Например: Книжная правая ориентация экрана)`

Все остальные случаи, в том числе ситуации, когда слово написано абсолютно верно, но все равно вызывает ошибку, предлагая исправить на само себя - попытайтесь поиграться со структурой предложения. Если это не помогает - проигнорируйте эту ошибку, и сообщите о ней [[[данному автору]]](https://t.me/amper_unlisted).

Добавление необдуманных записей в словарь может очень сильно испортить работу в будущем. Если есть сомнения - обратитесь с вопросом в наш чат.
:::

Варианты дополнения словаря:

- Явное указание слова

  ```
  "dictionary": [
    ... ,
    "коммит" // Плагин будет понимать слово "Коммит" и "коммит")
  ]
  ```

- Формы слова
  ```
  "dictionary": [
    ... ,
    "коммит(а|ов)" // Плагин будет понимать слова "Коммит", "коммита" и "коммитов")
    // Можно использовать в любом месте слова
  ]
  ```
- Исключение определённых блоков (Используя RegExp)
  ```
  "ignoreText":
   [
    ["---.*?---", "gsm"] // Игнорирует все что находится в блоке Frontmatter
   ],
  ```
