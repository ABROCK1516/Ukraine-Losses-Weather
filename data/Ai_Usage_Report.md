# Prompts used for AI to assist with this Assignment & Reflection

The prompts that were used and shaped the project.

---

**Session 1 – 16 Oct 2026: choosing a topic and data sources**

**1.** (assignment brief attached) I want to base my project on the Russia–Ukraine war, which I follow closely on the news and YouTube. My initial idea is to look at whether conditions on the ground, such as weather, relate to the losses each side reports. The questions I want to try answer is one around how russian equipent losses has changed over the war and personnel and how like the weather plays a part in effecting these losses, what limitations should I be aware of?

**2.** is there any interesting questions we could answer if we lets say combined daily losses with scraped weather, like would it not be valuable to then scrape/find a set of drove/weapons useage daily. so like the correlation is casualitees are higher when the weather is clearer and this would answer a question of what weapons are most/least effective in different weather patterns. or what other angles can we hit it from

**3.** I like the weather with losses either casualites or equipment losses but the point of this assignment is like so from the kaggle set of equipment losses what questions does that answer, then if we add the weather what further questions now arise and can be answered and possible with the combination of weather and the kaggle dataset could there potentially be a new angle of questions/ another scrape/dataset ect that answers a question

**4.** 2022 Russia Ukraine War so this has russian equipent losses and personsel losses. there is also a different kaggle set on daily missile strikes ( not sure if this is relevant)

**5.** Provide me with websites that contain ukrainian weather updates/patterns that I can view myself and pick the best one

**6.** I’ve chosen the 3-hourly observation pages for occupied Donetsk and Kharkiv. I’m leaning towards using it from 2023 because the data is a bit imcomplete from what ive quickly looked at and it seems to be more complete at the start of 2023 onwards; same with the kaggle one. What’s the strongest argument against that choice? For layer 3, I searched for daily clash data and found the ukranian general staff use a dashboard to monitor daily clashes. Is it suitable, or is there a better option?

**7.** Is it not better to have 2023 war data and 2023 weather onwards like, is it not important to have two full correltating war data sets and weather set. Did you confrim if the data of the weather goes the whole way from 2023 to current 2026

**Outcome**

Claude pointed out that “which weapons are most effective in each weather” can’t be answered from the losses data, because it doesn’t record what destroyed each item. I reframed the question as which loss categories vary with weather, in three layers: Kaggle alone → + weather → + a third dataset.

I chose the piterfm losses dataset (equipment + personnel) and pogodaiklimat.ru 3-hourly weather for occupied Donetsk (34519) and Kharkiv (34300), after comparing the sites Claude listed. I decided against the missile strikes dataset. I found ukraine.vefgreining.com for daily clash data.

When I asked whether the weather data was complete, Claude admitted it had only spot-checked it. Further checks found no data for most of 2022 and a gap for Donetsk in June–July 2023. Decided the weather analysis will use 2023 onwards, while keeping the full Kaggle data for Step 1.

**Session 2 – 18 Oct 2026: plan, engagement data and setup**

**8.** I’ve drafted a an assignment schedule plan: Step 1: load and check the Kaggle data, and turn running totals into daily losses. Step 2: scrape weather for two stations ethically, clean it, and make one row per day. Step 3: shift the Kaggle dates to the day of fighting and join the weather on date. Step 4: plot the merged data to answer both research questions, and list the issues. Write-up: observations, answers to the research questions, and a conclusion. Submit: a GitHub repo with the notebook, data, README and AI report, then demo it in class. Which steps depend on each other, and where do you see risks I haven’t planned for?

**9.** from the dashboard/website it seems i can only get the last year like from today to 1 year ago for daily engagments, where did you see i can get daily from may 2024 onwards?

**10.** (pasted output: rows with a value per year, 2022: 0, 2023: 313, 2024: 366, 2025: 365, 2026: 289)

**11.** I have never used Github so can you detail me what i should do and then the steps afterwards on what to finish/complete today.

**Outcome**

I drafted a two-week plan, and Claude flagged dependencies and risks. The engagement data’s purpose is to show whether bad weather means less fighting or less deadly fighting.

Error caught: Claude had said the engagement data ran from May 2024 onwards. This didn’t match what I could see on the dashboard. When I tested the data file in Colab, the history was stored under data["history"]["eng"] with a single start date, and values run from 22 Feb 2023 to 16 Oct 2026, with a value for every day.

Date alignment check: one news article (h.ua, 3 Oct 2026) (https://ua.news/en/war-vs-rf/rosiia-vtratila-za-dobu-na-fronti-shche-1-560-viiskovikh) reported 194 engagements on 2 Oct and 1,560 personnel losses. The engagement data has 194 on 2 Oct, while the Kaggle data has 1,560 on 3 Oct. So Kaggle dates are the day of reporting, and need shifting back one day to match the day of fighting. This check was later replaced: in Session 7 I couldn’t source the 1,560 figure, so I confirmed the shift with the UNN report instead.

**Session 3 – 20 Oct 2026: Step 1 dataset description**

**12.** Data types: the data column is stored as a object which means pandas views it as text i think however i could not find an explaination for why its an object, i just kept seeing people say everything in python is an object.

**13.** so am i able to use equipment even if it was only started in use/ like 2023 onwards such as cruise missles?

**14.** On 22 September 2023, headquarters of the Russian Black Sea Fleet at Sevastopol was attacked by Storm Shadow/SCALP cruise missiles launched by Su-24s of the Ukrainian Air Force. this is what i pulled online

**15.** (quoted part of Claude’s previous message about new categories starting with a high value) for this data is it possible to find the average so lets say ground robots gets added on day 550 of the war, could i divide the figure 1306 by 550 to get the average per day or would this just be an incorrect way of handling the data

**16.** I have done a review of my notebook and have tried to make sure that every heading is the right size and is bold, will you double check this and let me know if any corrections need to be made

**Outcome**

Notebook fixes: I checked the notebook against the brief and added the dataset description above the data notes. Claude then pointed out issues with heading levels, intro typos, the Kharkiv wording and comments in the setup cells, which I fixed myself.

Check cells: Claude wrote two check cells and explained each line. One confirms the dates match in both files; the other finds the first and last date each mostly-empty column has data. I ran them: the dates matched in every row, and the date ranges showed when each category was added, dropped or replaced.

Choosing loss categories: The final tests are: reported for the whole period, changes often enough, and linked to front-line weather.

Submarine date: Claude suggested that the submarines column starting on 14 Sep 2023 might match a strike in Sevastopol. My search found a different attack (22 Sep 2023, Black Sea Fleet headquarters). Claude then confirmed with a web search that the submarine Rostov-on-Don was hit on 13 Sep 2023, which fits the one-day reporting delay.

Averages: I asked whether a new category’s first value could be spread over the earlier days to get a daily average. Claude explained why not, using my data: it would give about 0.85 ground robots per day and it would invent figures for days with no reports.

**Session 4 – 20–22 Oct 2026: robots.txt, terms of use, scraping ethics and daily losses**

**17.** Today I’m checking robots.txt for pogodaiklimat.ru before scraping anything. I understand I need to find which rules apply to my scraper and whether weather.php is disallowed. Is there anything else I should check before fetching pages?

**18.** (quoted part of Claude’s previous message asking me to open robots.txt in the browser) this wont seem to load for me everytime i look it up

**19.** (attached a screenshot of the browser error “can’t reach this page”) the wbebsite is acting weird now

**20.** I cant seem to access the website at all, i tried edge and chrome and tried manually typing in the website address, why would i be blocked?

**21.** (followed by the robots.txt output from Colab) Yes im on hotspot and its not working - maybe thats the reason? last time i looked it up i was using my at home wifi. and yes it works in colab this is the output.

**22.** The first block of rules apply to me. No weather.php is not among them so we are safe to visit. No there is no crawl delay but we will use one to prevent overloading the website, if there was no delay then it would be obvious there is a bot scraping. can you explain to me more about the summary, what would be on the summary page that they wouldnt want it to be scraped

**23.** where are you seeing these clauses? where did you get that as im not seeingthat on the robot.txt

**24.** In what ways does this effect the robot.txt that i viewed?

**25.** (pasted the Russian text of sections 1–4 of the site’s user agreement, followed by:) TRANSLATE so i can match it with google translate

**26.** I’ve read the translated agreement and checked it with Google Translate. I think clause 3.5 matters because it seems to restrict sharing the site’s content, so I plan to keep the raw HTML in Drive and only publish extracted data. I also think clauses 2.9 and 3.6 explain why /summary/ is off limits. I plan to reference these in my ethics section. Is my reading of the clauses accurate?

**27.** From the translation, I read clause 3.5 as meaning I wouldnt be able to show it directly on my github and clause 3.6 as meaning the same as 3.5. Is that right? Also, instead of printing the whole agreement, I’d like the code to show only the clauses I reference. Does that make sense?

**28.** (quoted part of Claude’s previous message about inner, left and outer joins) how come we dont use join with outter then? This is how my lecturer taught us how to do it so im wondering what reasons are there to use the others

**29.** (attached a screenshot of the sorted table) just on this part of viewing the date by oldest, how come theres a column labelled ‘...’ and why does the personnel just have ‘ about’rather then figures

**30.** I cant acc find the value_counts() but the head and shape seem to confirm no missing values. there is a negative day - on day 457 tanks are at -2.0 - possibly due to inaccurate reports or over counting destoryed tanks ect?\
in the summary statistics the min figures are in negatives or 0, im not sure why explain. -2.000000 -14.000000 -10.000000 0.000000 0.000000\
median for drones is alot higher at 36 compared to tanks 5, this would make sense as there is well more wide usage of drones as they are cheaper and more effective then tanks

**Outcome**

Site access: I couldn’t reach the site in Edge or Chrome on my phone hotspot. Claude checked with its web tool that the site was up. The robots.txt request worked in Colab, and the site loaded on my home Wi-Fi, so the problem was my mobile network.

robots.txt: I ran the check in Colab and worked out that the general rules apply to my scraper, /weather.php isn’t disallowed and there’s no crawl delay.

Terms of use: Claude pointed me to the site’s user agreement. I had it translated, checked the translation with Google Translate, and worked out which clauses apply to my project. My first reading (26–27) linked /summary/ to clauses 2.9 and 3.6 and read 3.5 as only about sharing content. After checking, clauses 3.5 and 3.6 show /summary/ is a members-only section, which corrected Claude’s earlier guess. Because of clause 3.5, the raw HTML pages will stay in Google Drive and only the extracted data will go on GitHub.

Weather page structure: Claude loaded the March 2024 Donetsk page and pointed out that the times and the weather values are in two separate tables, that rows in italics are modelled estimates rather than real observations, that the page is UTF-8, and that the bot=2 URL parameter may answer the site’s “robot / alien / human” question. I still need to check all of these myself.

Daily losses: Claude explained the code to convert the dates, join the two files, sort by date, check for missing days and calculate daily losses with .diff(). After asking about the join types, I chose an outer join. I ran all the checks.

**Session 5 – 23 Oct 2026: fetching one page, the bot parameter and parsing one month**

**31.** I get a FileNotFoundError for raw_html/donetsk_2024_03.html. I saved the site’s page from my browser, so I think either the file is in the wrong place or I saved the wrong page. Is the code meant to download the page itself?

**32.** (followed by the full FileNotFoundError traceback from the fetch cell) explain whats wrong with the code so i can fix it myself

**33.** The raw_html folder now exists and the March 2024 Donetsk page has downloaded. My next step is to check the page’s encoding and table structure before writing the parser. Is there anything I should check first?

**34.** (followed by the output of the table-listing cell, run with bot=0) for the bot it came back with this. 74182 characters | 2 tables 53 rows 53 rows

**35.** I would consider by passing the human gate as ethical as its only for a student project, its not used in malicous intent and its only taking weather observations not super high value data, what should i be aware, is there any pushback?

**36.** I’ve considered your point that the bot field is an access limit. I’ve decided to use bot=2 because if I use bot then it  will severely limit the project, and I’ll record this decision and my reasoning in the ethics section.

**37.** Will we have to do translate it to english at some stage?

**38.** I can do that at the end i was just wondering

**39.** (pasted the output of march["wind_speed"].unique(), followed by:) An array is like a list isnt it? its like a structured/organised list?

**40.** there is a weird glitch in my github, colab notebook, where the words and the screen is all stuttery

**41.** im in edge and its in github

**42.** (attached a short video of the glitch, with no text)

**43.** I switched to Chrome and it works. I’ve committed the notebook. I think the repository also needs a README and the extracted CSVs, but not the raw HTML, because of clause 3.5. Is anything else expected in a project repository?

**Outcome**

Plan: I checked my progress against the Session 2 plan and found I was behind my inital plan.

Fetching one page: I had downloaded the site’s home page from my browser by mistake (Edge had also translated it). After diagnosing the error, I realised the code downloads the page itself. The first fetch cell failed because the raw_html folder didn’t exist; this was fixed with os.makedirs.

Page structure: I ran the charset, table-listing and bot-input cells. The page is UTF-8 and has two tables with no class: one with times and dates, the other with the 18 weather values, both with 243 rows.

The bot parameter: the form’s bot field means 0 = robot, 1 = alien, 2 = human (ticked by default). Claude suggested testing bot=0, and it returned only 53 rows instead of 243. I argued that answering “human” was ethical because the project is low-risk. Claude disagreed, because the field is an access limit and bot=2 misrepresents the scraper. I decided to use bot=2 because it allows me to analyse the datasets with enough and complete data that my project relies on, and recorded this in the ethics section.

**Session 6 – 24–25 Oct 2026: restructuring, parsing and cleaning**

(session opened with the updated project_context.md uploaded; no message)

**44.** (uploaded Ukraine_Losses_Weather.ipynb) This is how my noteboook is looking currently, i am going to move onto step 3 and i would like you to let me know if there is anything I should be aware of?

**45.** 1a. I don’t understand your point. Can you explain what the problem is, so I can decide whether to change it?\
1b. My observation: “With bot=0, the page returned only 53 rows, compared with 243 rows with bot=2. This suggests the site gives less data when it knows a bot is requesting it.” Is this accurate, and is anything missing?\
1c. I’m not sure which part of step2/3 you think needs fixing. Can you point to the specific cell?

**46.** (quoting Claude’s instruction E1 about checking 2022 pages in the browser) Can i check this in inspect mode on the site or do i have to run it in colab?

**47.** when i looked them up from the browser, it just brought me to the main section of the site, ill try something else

**48.** I expected there to be data about the weather for 2022 as the weather is unrelated to the invasion of ukraine\
The whole monthh is empty so its not related to the invasion?\
This supports starting both stations in january 2023 as 2023 has more complete and accurate data. Do you disagree? If so, state why.

**49.** my colab is quite slow and a bit laggy, do you think its worth creating a colab per research question?

**50.** My notebook is hard to follow, so I’ve drafted a new structure: Step 1 – dataset description; Step 2 – scraping; Step 3 – merge; Step 4 – analysis, with each step opening with its goal and how it links to my research questions, it basically resembles how the assignment brief is laid out. Does this cover everything in the brief, and is anything missing?

**51.** (quoting “Above the .describe() cell on the daily columns:”) I don’t have a .describe() cell for the daily columns. I think it should be code bit placed after cell. Is that right?

**52.** (uploaded Ukraine_Losses_Weather.ipynb) Review only step 1 - i took out a few bits of information that i deemed irellevant, if you have a strong case for it argue it.

**53.** Okay so now we know what the style is and weve changed up some of the observations, taken some stuff out, make some things shorter ect ect. now lets restructure our step 2. before we do, do you think i should change the subheadings to 1.8.1 or the 1.7.5 whats your opinion? which makes more sense

**54.** the reasons i gave the 1.71-1.74 is because those are the headings that fit step 1-4 in 1.7. don thtink it makes the same sense for the 1.82 ect

**55.** Lets do it

**56.** i think make it a little more clear - do any sections follow a 2.1.1 or 2.4.1 ect rule? and does the order of events make sense

**57.** i think the 2.1 hypothesis needs a change, as its not only about drones, apcs, tanks, will face difficulty in mud, heavy rain ect, so i dont think it makes sense for the hypothesis to limit to drones only

**58.** so i have restructured up to 2.4 - the bot observations cell

**59.** (screenshot of a NameError: ‘tables’ is not defined) so i restarted the session and was going line by line making sure it all worked. however in this section i recieved an error.

**60.** yeah i had forgooten to had the tables code below 2.3.3

**61.** i have two identical cells that find the tables, one under 2.3.2 and one under 2.3.3. Section 2.3.2 should decode the page and 2.3.3 should find the tables, so I’ll delete the one under 2.3.2. this is how i thinkg it should be, thoughts?

**62.** My cell fails because weather_row isn’t defined. I think I deleted the cell that selects one row from the weather table when I restructured. 

**63.** Next I’m cleaning the parsed data. My steps are: remove duplicate rows, convert times from UTC, then build daily summaries. I’m starting with the duplicates.

**64.** (pasted 2.9 outputs: 0 broken rows, (21474, 23), station counts, first rows)
Before running 2.9, I predicted it to have 21474 rows and 23 columns, since there are 23 categories, and I expected June and July 2023 to be empty for Donetsk. The output shows 0 broken rows and (21474, 23). Is my reasoning about June and July right?

**65.** (pasted duplicates check output) a few questions i hope you can help me answer: i know these are duplicates but why in some of the duplicates is there different figures for the pressure_sea and pressure_station

**66.** (pasted the 21 duplicate rows) just from looking at the output, i find 11362-11365 odd as they are exact duplicates, there is some outputs with just ho like you said too

**67.** (pasted output of the duplicate removal: (21461, 23), 0 duplicates left)

**68.** I would say keep Wind_dir - yes its about wind strength but that would be important factor to consider for drones/ firing shells ect. also why would humidity be an extra fog indicator? is there a certain level of humidity that comes with fpg==og

**69.** okay drop wind_dr, keep humidity

**70.** (pasted the check_columns list cell and its output)

**71.** (pasted the 2.10.3 inspection output)

**72.** in the process of cell pair 1 - the code output came back as (pasted KeyError: [‘precip_24h’] not found in axis)

**73.** (screenshot of the converted number columns’ dtypes)

**74.** (pasted the converted-values check output)

**75.** (uploaded Ukraine_Losses_Weather.ipynb) I’ve reviewed Step 2 myself. Every cell runs after a restart, and the outputs match what I expected except, will you do a review and let me know if i missed or did anything wrong ect ect

**76.** 1. we will do a but before we do how much extra work would b need and would it even be worth the effort for the extra accuracy?
2. this table makes sense to me.
3. would we be dropping alot of days? like do we have an estimate of how many days have less then 6 readings?

**77.** (pasted 21:00 UTC rows) for the utc_times. the output isnt what i was expecting i thought the time would be there likw 15:00 for example aswell unless im reading it wrong

**78.** anyway we can add that code to show the time into our main code cell then

**79.** how long will step 3 take in a rough estimate , step 2 seemed to take forever

**80.** I’m committing an AI log now. List every prompt I sent in this session word for word, without editing, shortening or leaving any out. I’ll write the outcomes myself.

**Outcome**

Notebook restructured at my request: I drafted a new structure with numbered sections matching the brief, a Goal/Assignment/Research-link opener for each step, and a markdown cell above every code cell. Claude checked it against the brief. I set the numbering rule: numbered headings are the steps listed in a section, unnumbered headings are checks.

Hypotheses: I broadened the 2.1 table beyond drones to armour, mud and rain. I argued for keeping wind direction and questioned the humidity–fog link; Claude explained the limits of each, and I chose to drop wind direction and keep humidity until it was tested.

Parsing and cleaning (2.9–2.11): Claude helped with the code and I wrote observations. I spotted the exact duplicate copies and the hidden times in the local-time output.

My decisions: UTC+3 for both stations (after Claude explained the cost of handling the clock change), the daily rules table, and the 6-reading cut-off after checking how many days it drops.

**Session 7 – 25–27 Oct 2026: merge, analysis and final review**

**81.** (uploaded Ukraine_Losses_Weather (1).ipynb)
I’m starting Step 3. My plan is to shift Kaggle dates back one day and then left-join the daily weather onto the losses data by date. Before starting, I checked that weather_daily.csv is saved after the final cleaning step. Does my Step 3 plan fit with how Step 2 ends?

**82.** I found a source from the UNN to help make sure the kaggle numbers are accurate/ as accurate as they can be

**83.** Since I’ve replaced the earlier article with the UNN report, I need to update the date-shift section. I think the markdown in data sources or somewhere in step 2 needs the new source and the check cell needs the 10 and 11 October figures. Is anything else affected?

**84.** Estimated time for Step 4?

**85.** I’ve decided to drop the extension. For Step 4, I want to compare losses across weather conditions. My concern is that losses also change with the season and the phase of the war. My idea for dealing with that is using a boxplot of the different weather patterns and comparing. What problems do you see with that approach?

**86.** for 4.2.1 the log needs to be changed as the log 10 to the power of 2 just looks a bit confusing and hard to read - what can this be changed to?

**87.** so MRLs and Air defence i think losses are smaller because they are usually more expensive so its harder to bring more out on the field once its been desytoryed. might be a potential reason.

**88.** (screenshots of the four bar plots)\
from my own knowledge i am surprised at the personnel loss one, usually when there is fog, cloudy days it means drones cant spot personnel/equipment or even other drones so. But personnel loss could be from what i say, the same amount of soliders may die but on foggy days it could be actual soliders killing rather then drones however this isnt like fully accurate. A reduction in overall equipment loss would sort of make sense as drones do alot of spotting and targeting for other drones/ artillery/ missle strikes ect

**89.** (pasted gust check output) Krarkiv at 13?

**90.** I think i need help you mentioned possibility of creating a breezy column, that makes sense to me but can you walk me through how I would implement this?

**91.** I’m keeping the bar plots and adding a scatter plot of  against relative loss, because it is continuous and a scatter plot shows whether there’s a trend rather than a split at one threshold. Is that a reasonable choice?

**92.** can i also change the bar chart colours, i think the blue and orange is a bit plain lookinhg - any suggestions that would suit the project

**93.** Starting 4.4 now. Tomorrow I’ll do a full check of the notebook myself. I’m planning to add a map of the two weather stations so the reader can see where the weather data comes from relative to the front line. Would that add value, or would something else help the reader more?

**94.** how much extra effort to answer RQ3?

**95.** So if i sent this to my lecturer would it not work because it has to load my drive and how would he be able to load it without my drive/ is there a way for it to load without my drive?

**96.** no that makes sense if its all visible in github.

**97.** would striking artillery be considered medium or short range drone capabilites? how far away is artillery from the front lines usually?

**Outcome**

Previous-session check: Before starting Step 3, I thought weather_daily.csv was saved after the final cleaning step, but checking my save point showed it had been saved before the dry-day fill. I moved the fill above the save and re-ran the notebook.

Date shift: I sourced the data from session 2 (https://ua.news/en/war-vs-rf/rosiia-vtratila-za-dobu-na-fronti-shche-1-560-viiskovikh) however I found the UNN to be a more reliable source so I replaced it with the 11 October General Staff report (UNN), whose totals minus the 10 October losses matched Kaggle’s 10 October row exactly, confirming Kaggle dates are report dates.

Step 3: the left join kept all 1,689 rows; Kharkiv has weather on 1,378 and Donetsk on 1,294. My outputs showed a quarter of days have only one 12-hour precipitation total, so the plan to drop those days was abandoned.

Step 4 design: Claude proposed comparing each day with its own month (relative loss) to control for season and the growth of losses over the war, along with the weather thresholds and the Kharkiv check. I asked for the log axis to show plain numbers. I dropped the research question 3 extension, checked the extra effort again and kept that decision.

Research question 1: the interpretations are mine: small infantry groups, the mobile front in 2022, APCs used in assaults, the expanding kill zone, and the cost of MRLs and air defence.

Research question 2: artillery, chosen as the comparison, changed most. The drone-spotting explanation and the fog/close-combat explanation for personnel are mine. My question about Kharkiv’s 13 gusts showed Kharkiv rarely records gusts, which led to the mean-wind (breezy) condition.


## Reflection on AI use

### What went well
- **The AI's checks found problems I would have missed.** It found that precipitation values were totals over hidden periods stored in the page's HTML, so adding them up would have counted the same rain twice, and it flagged a 320 mm "one-hour" value as an error. In the final clean-up it found a variable called `time` that replaced the `time` module, and a hypotheses table that the notebook referred to three times but didn't contain.
- **My own outputs corrected the AI.** My merged data showed that about a quarter of days have only one 12-hour precipitation total, so the AI's plan to drop those days would have lost too much data. My overlap check showed that rain, wind and fog don't mostly fall on the same days, which the AI had assumed. My question about Kharkiv having only 13 gusts showed that the two stations report wind differently.
- **I made the key decisions.** These include the numbering rule for headings, keeping humidity until it was tested, using UTC+3 after weighing the cost of handling the clock change, and dropping the research question 3 extension.

### What didn't go well
- **The AI sometimes presented assumptions as facts.** It claimed that rain, wind and fog mostly fall on the same days (disproved by my 4.4 check). I think sometimes the AI will come up with an idea or number and just present it as entirely true.
- **Too much at once.** Long edit lists would be overwhelming and sometimes irrelvant to what was necessary - seemed to create problems.
- **Dependence.** I did find I had to rely on AI to help me with the coding part and providing explainations on how it did the code and why it was done that why.
### What I would do differently
- Check every AI claim against my own data before accepting it, as I did successfully with the precipitation and overlap checks.
- Ask for smaller steps, and keep a source link for every figure I take from outside the data.
- Before the lab exam, where AI isn't allowed, practise writing the core code on my own.
