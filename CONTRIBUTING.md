# Contributing

## Что можно поправить

### 1. Классификация турниров (самое частое)

Файл `data/tournament_classification.json` определяет, какие турниры попадают на страницу каждой страны.

Структура:
```json
{
  "country_id": {
    "country_name": "Название",
    "main": [123, 456, 789],     // основные чемпионаты
    "student": [...],             // студенческие
    "school": [...],              // школьные
    "youth": [...],               // молодёжные
    "league": [...],              // лиги/этапы
    "mirror": [...],              // синхроны/асинхроны
    "special": [...]              // особые форматы
  }
}
```

На страницу страны попадают только турниры из `main`.

**Примеры правок:**
- Турнир неправильно классифицирован: переместите ID из одной категории в другую
- Турнир пропущен: добавьте ID в нужную категорию
- Лишний турнир: удалите ID

ID турнира -- это число из URL: `rating.chgk.info/tournament/12345` -> `12345`

### 2. Данные турниров

Файлы `data/countries/{country_id}.json` содержат результаты турниров, скачанные из API rating.chgk.info.

Если какого-то турнира нет в данных, но он есть в classification -- его нужно скачать. Запустите:

```bash
python3 fetch_worldwide.py  # скачает недостающие
```

Или откройте issue, и мы добавим.

### 3. Добавить новую страну

1. Найдите турниры на rating.chgk.info
2. Добавьте запись в `data/tournament_classification.json`
3. Скачайте данные: `python3 fetch_worldwide.py`
4. Перегенерируйте: `python3 build_worldwide.py`

## Файлы данных

| Файл | Страна | ID в classification |
|------|--------|---------------------|
| `data/countries/azerbaijan.json` | Азербайджан | 3 |
| `data/countries/armenia.json` | Армения | 4 |
| `data/countries/belarus.json` | Беларусь | 5 |
| `data/countries/bulgaria.json` | Болгария | 7 |
| `data/countries/uk.json` | Великобритания | 8 |
| `data/countries/germany.json` | Германия | 9 |
| `data/countries/georgia.json` | Грузия | 10 |
| `data/countries/israel.json` | Израиль | 11 |
| `data/countries/kazakhstan.json` | Казахстан | 13 |
| `data/countries/canada.json` | Канада | 14 |
| `data/countries/kyrgyzstan.json` | Кыргызстан | 16 |
| `data/countries/latvia.json` | Латвия | 17 |
| `data/countries/lithuania.json` | Литва | 18 |
| `data/countries/moldova.json` | Молдова | 19 |
| `data/countries/russia.json` | Россия | 21 |
| `data/countries/usa.json` | США | 22 |
| `data/countries/turkmenistan.json` | Туркменистан | 23 |
| `data/countries/uzbekistan.json` | Узбекистан | 25 |
| `data/countries/ukraine.json` | Украина | 26 |
| `data/countries/finland.json` | Финляндия | 27 |
| `data/countries/czechia.json` | Чехия | 29 |
| `data/countries/estonia.json` | Эстония | 31 |
| `data/countries/poland.json` | Польша | 99 |
| `data/countries/cyprus.json` | Кипр | 100 |
| `data/countries/switzerland.json` | Швейцария | 101 |

## Как сделать PR

1. Fork репозитория
2. Отредактируйте `data/tournament_classification.json` (и/или файлы в `data/countries/`)
3. Опишите в PR, что и почему поменяли
4. Если добавляете новый турнир, укажите ссылку на rating.chgk.info
