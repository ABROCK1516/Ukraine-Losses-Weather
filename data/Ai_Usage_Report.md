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


## Session 5 – 23 Oct 2026: fetching one page, the bot parameter and parsing one month

**32.**
> So whats the plan now

**33.**
> plan as it whats next work wise for this assignment that i can start doing now

**34.** *(pasted the error below and attached a copy of the site's home page that I had saved from my browser)*
> [Errno 2] No such file or directory: 'raw_html/donetsk_2024_03.html'

**35.** *(followed by the full FileNotFoundError traceback from the fetch cell)*
> explain whats wrong with the code so i can fix it myself

**36.**
> yes that has been created whats next?

**37.** *(followed by the output of the cell that prints the 18 weather cells)*
> for the bot it came back with this. 74182 characters | 2 tables 53 rows 53 rows
>
> weather came back with this

**38.**
> I would consider by passing the human gate as ethical as its only for a student project, its not used in malicous intent and its only taking weather observations not super high value data

**39.**
> Will we have to do translate it to english at some stage?

**40.**
> we can do that at the end i was just wondering

**41.** *(pasted the output of `march["wind_speed"].unique()`, followed by:)*
> An array is like a list isnt it? its like a structured/organised list?

**42.**
> there is a weird glitch in my github, colab notebook, where the words and the screen is all stuttery

**43.**
> im in edge and its in github

**44.** *(attached a short video of the glitch, with no text)*

**45.**
> i switched to chrome and it works. okay so after comitting our colab file whats next to do in github

### Outcome
- **Plan:** Claude set out a day-by-day plan up to submission and flagged that I was about a day behind.
- **Fetching one page:** I had downloaded the site's home page from my browser by mistake (Edge had also translated it), so Claude explained that the code downloads the page itself. Claude's first fetch cell failed because it expected me to create the `raw_html` folder by hand; Claude fixed it with `os.makedirs`.
- **Page structure:** I ran the charset, table-listing and bot-input cells. The page is UTF-8 and has two tables with no class: one with times and dates, the other with the 18 weather values, both with 243 rows. 
- **The bot parameter:** the form's `bot` field means 0 = robot, 1 = alien, 2 = human (ticked by default). Claude suggested testing `bot=0`, and it returned only 53 rows instead of 243. I argued that answering "human" was ethical because the project is low-risk. Claude disagreed, because the field is an access limit and `bot=2` misrepresents the scraper.

- ## Session 6 (24–25 October 2026)

**46.** *[Quoting Claude's instruction E1 about checking 2022 pages in the browser]* Can i check this in inspect mode on the site or do i have to run it in colab?

**47.** when i looked them up from the browser, it just brought me to the main section of the site, ill try something else

**48.** 1. I expected there to be data about the weather for 2022 as the weather is unrelated to the invasion of ukraine
2. The whole month is empty so its not related to the invasion?
3. This supports starting both stations in january 2023 as 2023 has more complete and accurate data. do you disagree if so state why

**49.** my colab is quite slow and a bit laggy, do you think its worth creating a colab per research question?


**50.** okay before we do anything else. would it be worth creating a new colab and copy and pasting what we need/whats been added into this new one and also taking stuff out if we dont need it. right now the colab just seems very messy and has like no clear structure and flow, this is something i would rather have ready then last minute. i want to try get the whole assignment done soon. I think we need to think to think of a clear strutcure that matches the assignment but is also easy for the reader to understand what section they are on, what the section is doing, how it relates to the research and assignment too. before doing anything else - lets go back to the drawing board and see what we can come up with

**51.** *[Uploaded Ukraine_Losses_Weather (5).ipynb]* Okay that makes sense so we'll stay in the same colab.  This is the file right now. We need to determine if all content in it is necessary, how maybe we can rewrite some sections to make the flow more clear and structured.

**52.** the reasons i gave the 1.71-1.74 is because those are the headings that fit step 1-4 in 1.7. don thtink it makes the same sense for the 1.82 ect

**53.** i think make i will make a little more clear - do any sections follow a 2.1.1 or 2.4.1 ect rule? and does the order of events make sense

**54.** okay can i start working now on it

**55.** so i have restructured up to 2.4 - the bot observations cell

**56.** *[Screenshot of a NameError: 'tables' is not defined]* so i restarted the session and was going line by line making sure it all worked. however in this section i recieved an error.

**57.** yeah i had forgooten to had the tables code below 2.3.3

**58.** *[Screenshot of the 2.3.3 cells]* like this?

**59.** okay i think i have this mixed up. 2.3.2 is reading and decoding the pages followed by a code cell. *[pasted the 2.3.3 and "Checking the Cells in One Row" markdown and the tables code cell]* now i have two code blocks that follow eachpther as in their the exact same coding blocks

**60.** i dont think i have the code for the weather_row

**61.** okay lets work on chunk 3

**62.** grand lets get to work

**63.** *[Pasted duplicates check output]* a few questions i hope you can help me answer: i know these are duplicates but why in some of the duplicates is there different figures for the pressure_sea and pressure_station

**64.** *[Pasted the 21 duplicate rows]* just from looking at the output, i find 11362-11365 odd as they are exact duplicates

**65.** in the process of cell pair 1 - the code output came back as *[pasted KeyError: ['precip_24h'] not found in axis]*

**66.** *[Uploaded Ukraine_Losses_Weather (7).ipynb]* lets do a review of our step 2 and let me know if everything is in the right place and outputs are correct

**67.** *[Pasted 21:00 UTC rows]* for the utc_times. the output isnt what i was expecting i thought the time like you said would be there aswell unless im reading it wrong

**68.** anyway we can add that code to show the time into our main code cell then

**69.** how long will step 3 take, step 2 seemed to take forever

### Outcome
- **Notebook restructured** at my request (95): numbered sections matching the brief, a Goal/Assignment/Research-link opener for each step, and a markdown cell above every code cell. Claude proposed the structure; I set the numbering rule (101): numbered headings are the steps listed in a section, unnumbered headings are checks.
- **Step 2 review:** Claude found the test-page loop had been deleted, a missing heading, and an out-of-date ethics line, and made all download cells safe to re-run.
- **Hypotheses:** I broadened the 2.1 table beyond drones to armour, mud and rain (106). I argued for keeping wind direction and questioned the humidity–fog link (119); Claude explained the limits of each, and I chose to drop wind direction and keep humidity until it was tested.
- **Parsing and cleaning (2.9–2.11):** Claude helped with the code and I wrote observations. I spotted the exact duplicate copies (117) and the hidden times in the local-time output (133).
- **My decisions:** UTC+3 for both stations (131, after Claude explained the cost of handling the clock change), the daily rules table, and the 6-reading cut-off after checking how many days it drops.
