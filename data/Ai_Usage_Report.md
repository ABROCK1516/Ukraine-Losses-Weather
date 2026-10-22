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

---

- ## Session 3 – 20 Oct 2026: Step 1 dataset description 

**13.**
> 'Add a brief text description of your dataset to your iPython notebook.' do you think we have done this or shall we add this just above the 'data notes'

**14.**
> Data types: the data column is stored as a object which means pandas views it as text i think however i could not find an explaination for why its an object, i just kept seeing people say everything in python is an object.

**15.**
> so are we able to use equipment even if it was only started in use/ like 2023 onwards such as cruise missles?

**16.**
> On 22 September 2023, headquarters of the Russian Black Sea Fleet at Sevastopol was attacked by Storm Shadow/SCALP cruise missiles launched by Su-24s of the Ukrainian Air Force. this is what i pulled online

**17.** *(quoted part of Claude's previous message about new categories starting with a high value)*
> for this data is it possible to find the average so lets say ground robots gets added on day 550 of the war, could i divide the figure 1306 by 550 to get the average per day or would this just be an incorrect way of handling the data

### Outcome
- **Notebook fixes:** Claude reviewed the notebook and gave copy-paste fixes for heading levels, intro typos, the Kharkiv wording and comments in the setup cells. I applied them. 
- **Check cells:** Claude wrote two check cells and explained each line. One confirms the dates match in both files; the other finds the first and last date each mostly-empty column has data. I ran them: the dates matched in every row, and the date ranges showed when each category was added, dropped or replaced.
- **Choosing loss categories:** Claude suggested three tests for which categories to use in the weather analysis: reported for the whole period, changes often enough, and linked to front-line weather.
- **Submarine date:** Claude suggested that the `submarines` column starting on 14 Sep 2023 might match a strike in Sevastopol. My search found a different attack (22 Sep 2023, Black Sea Fleet headquarters). Claude then confirmed with a web search that the submarine Rostov-on-Don was hit on 13 Sep 2023, which fits the one-day reporting delay.
- **Averages:** I asked whether a new category's first value could be spread over the earlier days to get a daily average. Claude explained why not, using my data: it would give about 0.85 ground robots per day and it would invent figures for days with no reports.


## Session 4 – 20–22 Oct 2026: robots.txt, terms of use, scraping ethics and daily losses

**18.**
> lets make a start

**19.** *(quoted part of Claude's previous message asking me to open robots.txt in the browser)*
> this wont seem to load for me everytime i look it up

**20.** *(attached a screenshot of the browser error "can't reach this page")*
> the wbebsite is acting weird now

**21.**
> I cant seem to access the website at all, i tried edge and chrome and tried manually typing in the website address, why would i be blocked?

**22.** *(followed by the robots.txt output from Colab)*
> Yes im on hotspot and its not working - maybe thats the reason? last time i looked it up i was using my at home wifi. and yes it works in colab this is the output.

**23.**
> The first block of rules apply to me. No weather.php is not among them so we are safe to visit. No there is no crawl delay but we will use one to prevent overloading the website, if there was no delay then it would be obvious there is a bot scraping. can you explain to me more about the summary, what would be on the summary page that they wouldnt want it to be scraped

**24.**
> where are you seeing these clauses? where did you get that as im not seeingthat on the robot.txt

**25.**
> does this change our layout for the robot.txt in the colab or?

**26.** *(pasted the Russian text of sections 1–4 of the site's user agreement, followed by:)*
> TRANSLATE

**27.**
> the site works now that im at home usinb my own wifi. do i need to put parts of the user agreement on my colab or?

**28.**
> ive no idea what you want me to do next. in terms of the user agreement and the ethics

**29.**
> what do the clauses mean and would it not be worth having the code just have the range frpm the list be about the clauses we're mentioning?

**30.** *(quoted part of Claude's previous message about inner, left and outer joins)*
> how come we dont use join with outter then?

**31.** *(attached a screenshot of the sorted table)*
> just on this part of viewing the date by oldest, how come theres a column labelled '...' and why does the personnel just have ' about'rather then figures

**32.**
> 1. I cant acc find the value_counts() but the head and shape seem to confirm no missing values.
> 2. yes there is a negative day - on day 457 tanks are at -2.0 - possibly due to inaccurate reports or over counting destoryed tanks ect?
> 3. in the summary statistics the min figures are in negatives or 0, im not sure why explain. -2.000000 -14.000000 -10.000000 0.000000 0.000000
> 4. median for drones is alot higher at 36 compared to tanks 5, this would make sense as there is well more wide usage of drones as they are cheaper and more effective then tanks

### Outcome
- **Site access:** I couldn't reach the site in Edge or Chrome on my phone hotspot. Claude checked with its web tool that the site was up. The robots.txt request worked in Colab, and the site loaded on my home Wi-Fi, so the problem was my mobile network.
- **robots.txt:** I ran the check in Colab and worked out that the general rules apply to my scraper, `/weather.php` isn't disallowed and there's no crawl delay. 
- **Terms of use:** Claude found and read the site's user agreement, which I hadn't known about. It corrected its own earlier guess about why `/summary/` is disallowed (it's a members-only section, clauses 2.9 and 3.6). Claude translated the agreement and I checked the translation with Google Translate. Because of clause 3.5, the raw HTML pages will stay in Google Drive and only the extracted data will go on GitHub.
- **Weather page structure:** Claude loaded the March 2024 Donetsk page and pointed out that the times and the weather values are in two separate tables, that rows in italics are modelled estimates rather than real observations, that the page is UTF-8, and that the `bot=2` URL parameter may answer the site's "robot / alien / human" question. I still need to check all of these myself.
- **Daily losses:** Claude explained the code to convert the dates, join the two files, sort by date, check for missing days and calculate daily losses with `.diff()`. After asking about the join types, I chose an outer join. I ran all the checks.
