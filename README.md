# SG-Graduate-Employment-Dashboard
This is a dashboard describing trends in employment rates, median salary and salary gap between the years 2020-2023 for local graduates in Singapore from NUS, NTU, SIT, SUSS, SUTD. 

The dashboard revealed accurate and key insights such as:
1. Top 3 earning majors: this highly aligns with the overall trend in the job market now. With AI boom, healthcare related professions are one of the least replacable.
2. Top 3 majors by salary gap: highly aligns with factual sentiments as some computing students be earning big bucks while some do not RIP.

# Data Cleaning
1.For greater contextual relevance, I only focused on 2020-2023.

2.I filtered out irrelevant schools/institutions

3.I standardised a set of degree names with the following logic as I realised that the degrees had: long names, joint degrees, random specialisations, inconsistent description across institutions. The standardisation was done through the following logic:
1) School based classification was given the highest priority as school names are usually more stable than degree names, and often already represent a faculty/discipline. (eg. medicine, law) So if school clearly indicates a discipline, we trust it immediately.
2) Degree based direct keywords: some rows have weird schools like joint programs (culinary school of america x SIT LOL). So if school does not trigger, I try to match with key words in degree (eg. engineering, computing, business etc)
3) Degree based group lists: I create related word lists for matching (eg. science = {chemistry, physics, biology, mathematics, biomedical, data science, etc.})
This was also intentionally done for Bachelor of Sciences as I felt that using "science" as a blanket statement over all BoS degree is highly unrepresentative due to the diverse nature of degrees under BoS (eg. food technology cannot be the same as nursing...)
4) The remaining were categorised as science

The above branching logic was realised through M scripting.

# Dashboard
I wanted a direct representative view of the top 3 majors with highest earnings, employment and smallest salary gap that could be viewed per school.

To realise the top 3 logic, I created measures by first ranking the majors by earnings/employment rate/ salary gap. Then another measure to capture the top 3 which is displayed in a multirow card.

To enable switching between schools, a star schema was created to have relevant slicers.

<img width="2157" height="1209" alt="image" src="https://github.com/user-attachments/assets/40e28492-ab0c-4c63-a8ae-fccf3d8aae20" />


# Trouble Shooting
This is a poorly formatted CSV that caused conversion type error when I attempted to load my cleaned and processed schema data. Based on the hints from the error message that suggested issues with the date conversion, I utilised keep error on my latest step as well as the change type step. It turns out that there was an irrelevant string that hindered the type conversion.

I overlooked this error as it occured very upstream whilst I was filtering the data. As the CSV file contained a lot of rows, I did not load all rows to inspect before filtering, which led to unwanted random year rows being kept
<img width="537" height="502" alt="image" src="https://github.com/user-attachments/assets/70534458-772f-4b2b-bf30-56c80bdde079" />

But I eventually managed to fix it by changing the filter logic in the M script instead of in the list of actions (cuz that js crashed everything downstream).
