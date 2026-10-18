# Prompts used for AI to assist with this Assignment & Reflection

The prompts that were used and shaped the project, copied word for word.

---

## Session 1 – 16 Oct 2026: choosing a topic and data sources

**1.** *(assignment brief attached)*
> I want to do something with ukraine/russia war related, like potential weapons or idk what ideas can we brain storm up. I have an interest in this and follow a'lot of it on the news or youtube channels but not sure whats out there.

**2.**
> is there any interesting questions we could answer if we lets say combined daily losses with scraped weather, like would it not be valuable to then scrape/find a set of drove/weapons useage daily. so like the correlation is casualitees are higher when the weather is clearer and this would answer a question of what weapons are most/least effective in different weather patterns. or what other angles can we hit it from

**3.**
> I like the weather with losses either casualites or equipment losses but the point of this assignment is like so from the kaggle set of equipment losses what questions does that answer, then if we add the weather what further questions now arise and can be answered and possible with the combination of weather and the kaggle dataset could there potentially be a new angle of questions/ another scrape/dataset ect that answers a question

**4.**
> 2022 Russia Ukraine War so this has russian equipent losses and personsel losses. there is also a different kaggle set on daily missile strikes ( not sure if this is relevant)

**5.**
> Provide me with websites that contain ukrainian weather updates/patterns that I can view myself and pick the best one

**6.**
> Okay so we will 100% use the 3-hourly observation pages as the data it provides is exacvtly what is needed to tell us the answers we want. we have 2 weeks so we have time to work on this. Occupied Donetsk is what we can label it is. also about the cities is it better to limit the data from 2024 to now so we can use Donetsk and Kharkiv. or do you think its important to have the full war data. also for layer 3 provide me wit the site or what is needed for the daily clashes too

**7.**
> Is it not better to have 2023 war data and 2023 weather onwards like, is it not important to have two full correltating war data sets and weather set. Did you confrim if the data of the weather goes the whole way from 2023 to current 2026

### Outcome
- AI pointed out that "which weapons are most effective in each weather" can't be answered from the losses data, because it doesn't record what destroyed each item. Reframed the question as which loss categories vary with weather, in three layers: Kaggle alone → + weather → + a third dataset.
- Helped me chose the piterfm losses dataset (equipment + personnel) and pogodaiklimat.ru 3-hourly weather for occupied Donetsk (34519) and Kharkiv (34300). Decided against the missile strikes dataset.
- When I asked whether the weather data was complete, AI admitted it had only spot-checked it. Further checks found no data for most of 2022 and a gap for Donetsk in June–July 2023. Decided the weather analysis will use 2023 onwards, while keeping the full Kaggle data for Step 1.

---

## Session 2 – 18 Oct 2026: plan, engagement data and setup

**8.**
> Before I start to work on it and draft an email to send off, lets confirm a clear plan of action

**9.**
> from the dashboard/website it seems i can only get the last year like from today to 1 year ago for daily engagments, where did you see i can get daily from may 2024 onwards?

**10.** *(pasted output: rows with a value per year, 2022: 0, 2023: 313, 2024: 366, 2025: 365, 2026: 289)*

**11.**
> Okay reread that the assignment brief says and tell me is there any parts i can start working on for the assignment today

**12.**
> I have never used Github so can you detail me what i should do and then the steps afterwards on what to finish/complete today.

### Outcome
- Agreed a two-week plan. The engagement data's purpose is to show whether bad weather means less fighting or less deadly fighting.
- **AI error caught:** AI had said the engagement data ran from May 2024 onwards. This didn't match what I could see on the dashboard. When I tested the data file in Colab, the history was stored under `data["history"]["eng"]` with a single start date, and values run from 22 Feb 2023 to 16 Oct 2026, almost complete.
- **Date alignment check:** one news article (h.ua, 3 Oct 2026) reported 194 engagements on 2 Oct and 1,560 personnel losses. The engagement data has 194 on 2 Oct, while the Kaggle data has 1,560 on 3 Oct. So Kaggle dates are the day of reporting, and need shifting back one day to match the day of fighting.
