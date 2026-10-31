# Russian Equipment & Personnel Losses & Front-line Weather

*Data Acquisition and Preprocessing – Individual Project*
**Alex Brock | C23426432 | TU912/4 | TU Dublin**

This project combines Kaggle's daily figures for Russian equipment and personnel losses in the war in Ukraine with weather observations scraped from two stations near the front line. It tests whether daily losses vary with rain, freezing temperatures, wind and low visibility.

## Research questions

1. **Kaggle data alone:** How have daily losses changed over the course of the war? Has the mix of equipment lost changed, and has the ratio of personnel to vehicles lost changed over time?
2. **Adding weather:** Do daily losses vary with weather conditions such as rain, freezing temperatures, wind and low visibility? Which loss categories are most affected?

## Main findings

- **Research question 1:** losses shifted from armour to drones and artillery. Tank and APC losses fell sharply in 2025, drone losses grew about 280 times from 2022 to 2026, and about eleven times more personnel were lost per armoured vehicle in 2026 than in 2022.
- **Research question 2:** on rainy, windy and low-visibility days, field artillery losses are about a quarter lower and drone losses about a fifth lower than on other days in the same month, at both weather stations. Armour and personnel losses barely change.

All loss figures are Ukrainian claims and have not been independently verified. The results show which losses go with which weather, not what caused them.

## Repository contents

| File or folder | What it is |
|---|---|
| `Ukraine_Losses_Weather.ipynb` | The notebook: Steps 1–4, with all outputs and plots |
| `data/raw/` | The two Kaggle CSV files (see the licence note below) |
| `data/processed/weather_daily.csv` | The scraped weather, one row per day for both stations (1,389 days × 25 columns) |
| `ai_usage_report.md` | Every AI prompt used in the project, with outcomes and a reflection |
| `README.md` | This file |

The raw weather pages (HTML) are **not** included: the site's terms (clause 3.5) don't allow its pages to be republished. Only the weather data extracted from them is shared.

## Notebook structure

| Step | What it does | Marks |
|---|---|---|
| Step 1 | Imports the Kaggle data, assesses its structure, types and values, and turns running totals into daily losses | 20 |
| Step 2 | Scrapes 3-hourly weather for occupied Donetsk (station 34519) and Kharkiv (station 34300), January 2023 – October 2026, cleans it and makes one row per day | 40 |
| Step 3 | Shifts the Kaggle dates back one day (report date → day of fighting) and left-joins the weather on `date` | 20 |
| Step 4 | Seaborn plots for both research questions, a check with the second station, and the issues in the merged data | 20 |

Libraries used: `pandas`, `urllib.request`, `BeautifulSoup` (bs4), `seaborn` and `matplotlib`.

## Data sources

**Losses:** ["2022 Russia Ukraine War" by piterfm](https://www.kaggle.com/datasets/piterfm/2022-ukraine-russian-war), Kaggle. Two CSV files of daily cumulative Russian equipment and personnel losses, as reported by official Ukrainian sources. Downloaded on 16 October 2026 (report dates 25 February 2022 – 10 October 2026)..
**Weather:** Weather data from [Pogoda i Klimat](http://www.pogodaiklimat.ru) (Источник: сайт [«Погода и Климат»](http://www.pogodaiklimat.ru)). 3-hourly observations scraped from the site's weather archive (`weather.php`) for station 34519 (Donetsk) and station 34300 (Kharkiv).

**Date check (Step 3.1):** [UNN, General Staff loss report of 11 October 2026](https://unn.ua/en/amp/the-general-staff-reported-the-number-of-russian-troops-and-pieces-of-equipment-destroyed-over-the-past-day), used to confirm that Kaggle dates are report dates.

## Scraping ethics

- **robots.txt:** `/weather.php`, the only page requested for data, is not disallowed, and no crawl delay is set.
- **Terms of use:** the site is used for non-commercial coursework (clause 3.1); its pages are not republished (clause 3.5); the members-only Summary section is not used (clause 3.6); the source is credited with a link (clause 3.7).
- **Requests:** each page was downloaded once, saved, and read from the saved copy afterwards, with a 3-second pause between requests and a User-Agent identifying the scraper as a student project.
- **The `bot` parameter:** the site's form asks whether the visitor is a robot, an alien or a human. Answering "robot" returns only the latest week, so the scraper answers "human" (`bot=2`, the form's default). This was approved by my lecturer on 23 October 2026.

## AI use

AI (Claude) was used for help with code, explanations and checking, as allowed by the brief. Every prompt is listed word for word in [`ai_usage_report.md`](ai_usage_report.md), with what came out of each session and a reflection at the end.
