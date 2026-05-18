# chgk_worldwide

Statistics dashboard for national "What? Where? When?" (ЧГК) championships across 25 countries.

**Live site: [imangulova.github.io/chgk-worldwide](https://imangulova.github.io/chgk-worldwide/)**

## Features

- Interactive SVG world map with real country outlines
- Per-country championship statistics (winners, podiums, team rankings)
- Two viewing modes: overall standings vs national championship standings
- Cross-country stats: travelers (most countries played), multi-country medalists
- "Iron men" -- players who never missed a single championship
- Year filters, dark/light theme

## Countries covered

Azerbaijan, Armenia, Belarus, Bulgaria, Canada, Cyprus, Czechia, Estonia, Finland, Georgia, Germany, Israel, Kazakhstan, Kyrgyzstan, Latvia, Lithuania, Moldova, Poland, Russia, Switzerland, Turkmenistan, UK, Ukraine, USA, Uzbekistan

## Data source

All data from [rating.chgk.info](https://rating.chgk.info) API.

## How to rebuild

```bash
# 1. Fetch data (requires internet, ~10 min)
python3 fetch_worldwide.py

# 2. Classify tournaments
python3 classify_tournaments.py

# 3. Generate HTML pages
python3 build_worldwide.py
```

## Author

Amal Imangulov -- [imangulovamal@gmail.com](mailto:imangulovamal@gmail.com)
