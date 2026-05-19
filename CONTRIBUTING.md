# Contributing

## Структура данных

```
data/
├── tournament_classification.json   # какие турниры в какой категории
├── db/
│   ├── players.json                 # {id: "Имя Фамилия", ...}
│   ├── teams.json                   # {id: {"name": "...", "town": "...", "town_id": N}, ...}
│   ├── russia/
│   │   ├── meta.json                # страна, town_ids
│   │   ├── tournaments.json         # [{id, name, date, questions}, ...]
│   │   └── results/
│   │       ├── 22.json              # результаты турнира 22
│   │       ├── 76.json
│   │       └── ...
│   ├── uk/
│   │   ├── meta.json
│   │   ├── tournaments.json
│   │   └── results/
│   │       └── ...
│   └── ...
```

## Что можно поправить

### 1. Классификация турниров (самое частое)

Файл `data/tournament_classification.json` определяет, какие турниры попадают на страницу каждой страны.

На страницу попадают только турниры из категории `main`. Остальные категории: `student`, `school`, `youth`, `league`, `mirror`, `special`.

**Примеры правок:**
- Турнир неправильно классифицирован: переместите ID из одной категории в другую
- Турнир пропущен: добавьте ID в `main`
- Лишний турнир: удалите ID

ID турнира -- число из URL: `rating.chgk.info/tournament/12345` -> `12345`

### 2. Результаты турнира

Файл `data/db/{страна}/results/{tournament_id}.json` содержит результаты одного турнира:
```json
[
  {"pos": 1, "team_id": 4730, "score": 35, "roster": [29787, 21235, ...], "flags": [50]},
  {"pos": 2, "team_id": 935, "score": 33, "roster": [31682, ...]},
  ...
]
```

- `pos` -- место
- `team_id` -- ID команды (расшифровка в `teams.json`)
- `score` -- количество взятых вопросов
- `roster` -- ID игроков (расшифровка в `players.json`)
- `flags` -- флаги зачёта (50 = зачёт чемпионата страны)

### 3. Игроки и команды

- `data/db/players.json` -- словарь `{id: "Имя Фамилия"}`
- `data/db/teams.json` -- словарь `{id: {"name": "Команда", "town": "Город", "town_id": N}}`

### 4. Добавить новую страну

1. Найдите турниры на rating.chgk.info
2. Создайте папку `data/db/{slug}/` с `meta.json`, `tournaments.json`, `results/`
3. Добавьте запись в `data/tournament_classification.json`
4. Обновите `build_worldwide.py` (slugs, flags, colors)
5. Перегенерируйте: `python3 build_worldwide.py`

## Страны

| Папка | Страна | ID |
|-------|--------|-----|
| `azerbaijan` | Азербайджан | 3 |
| `armenia` | Армения | 4 |
| `belarus` | Беларусь | 5 |
| `bulgaria` | Болгария | 7 |
| `uk` | Великобритания | 8 |
| `germany` | Германия | 9 |
| `georgia` | Грузия | 10 |
| `israel` | Израиль | 11 |
| `kazakhstan` | Казахстан | 13 |
| `canada` | Канада | 14 |
| `cyprus` | Кипр | 100 |
| `kyrgyzstan` | Кыргызстан | 16 |
| `latvia` | Латвия | 17 |
| `lithuania` | Литва | 18 |
| `moldova` | Молдова | 19 |
| `poland` | Польша | 99 |
| `russia` | Россия | 21 |
| `switzerland` | Швейцария | 101 |
| `turkmenistan` | Туркменистан | 23 |
| `usa` | США | 22 |
| `uzbekistan` | Узбекистан | 25 |
| `ukraine` | Украина | 26 |
| `finland` | Финляндия | 27 |
| `czechia` | Чехия | 29 |
| `estonia` | Эстония | 31 |

## Как сделать PR

1. Fork репозитория
2. Отредактируйте нужный файл
3. Опишите в PR, что и почему поменяли
4. Если добавляете турнир, укажите ссылку на rating.chgk.info
