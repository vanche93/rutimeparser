# Общие сведения

Данный модуль содержит базовый класс и упрощающие работу с ним функции для извлечения даты и времени из текста на русском языке.

# Использование

Примеры ниже приведены для 2 апреля 2017 года.

## Извлечение даты и времени

```python
>>> from timeparser import parse_time
>>> parse_time('завтра')
datetime.date(2017, 4, 3)
>>> parse_time('завтра утром')
datetime.datetime(2017, 4, 3, 9, 0)
>>> parse_time('Напомни мне завтра утром составить список дел.')
datetime.datetime(2017, 4, 3, 9, 0)
```

## Извлечение текста, не относящегося к дате и времени

```python
>>> from timeparser import get_clear_text, get_last_clear_text
>>> get_clear_text('Напомни мне завтра утром составить список дел.')
'напомни мне составить список дел'
>>> get_last_clear_text('Напомни мне завтра утром составить список дел.')
'составить список дел'
```

# Неявные ситуации

* `утром` - в 09:00
* `днём` - в 15:00
* `вечером` - в 21:00
* `ночью` - в 03:00
* `на следующей неделе` - на следующей неделе в понедельник.
* `через неделю` - ровно через 7 суток.
* `через неделю утром` - через 7 дней утром.
* `в следующем месяце` - 1 число следующего месяца.

Больше примеров в [tests.py](tests.py)

# API reference

## timeparser.parse_time

**Возвращаемые значения:**
* datetime.date
* datetime.datetime
* None

**Возможные исключения:**
* `ValueError: day is out of range for month` - передана неверная дата (например, 30 февраля).
* `ValueError: Please, set text or words for TimeParser.` - передана пустая строка.

## TODO

* Составить документацию к базовому классу
* Перейти на `pymorphy`
* Добавить поддержку AM/PM (например, "в два часа дня")