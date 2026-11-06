## Table of Contents

- [Overview](#overview)
- [Project Goals](#project-goals)
- [Core Features](#core-features)
- [Deployment](#deployment)
- [User Guide](#user-guide)
- [Community Feedback](#community-feedback)
- [Developer Guide](#developer-guide)
- [Development History](#development-history)
- [Continuous Integration](#continuous-integration)
- [Walkthrough Videos](#walkthrough-videos)
- [Team](#team)




Development Document for Word Cloud Web Application:
Overview:
	A webpage where users can upload text, to be generated into word cloud data (word frequency dictionaries) that can be displayed in various ways and with tools for sharing, research, commenting, and building datasets.

Organization: LittNebula (literature in latin = Littera (Litt), Cloud in latin = Nebula)



 ======================== To Do ========================
Priority:
Github Organization HomePage repo (Org Homepage)
“The home page for your organization should evolve over time to reflect the most recent state of your project. To begin with, the home page should provide a good description of the goals of the project, what the system should eventually provide, and screen shots of the mockup pages you plan to use as a basis for your final project. “
Design simple mockup visuals for User Homepage, User Login, Front Landing Page, Admin View of Cloud Data, Cloud Data display page, Cloud Data Add/Edit page,
Github Project Repo (source code)
Use Next Js Template and create mock up pages
Deploy to vercel
Design and debug Word Cloud Generator function:
Given plain text string, split into array of unique words, count the number of times the same word shows up, create a dictionary or json object the stores key:value as “word”:”count”
Save the json object to database
Implement Word Cloud Visualizer
References: https://github.com/boakham/d3-cloud-ts, https://medium.com/react-courses/create-a-word-cloud-data-visualization-chart-with-d3js-reactjs-and-typescript-969c63506856 
Later: 
Design Landing page for guests 
Design Registration, Login / Logout pages
Design User Homepage
Design Admin Homepage
Design Add Word Cloud data page
Design Edit Word Cloud data page (similar to add but with extra options, including delete option)
Design View Word Cloud data page: Display wordcloud as both cluster and a simple list of words
Provide support for languages that use alphabetical lexicon: Spanish, French, German,
Provide support for common languages in UHM, Japanese , Korean, Hawaiian, 
Provide support for hybrid languages: Hawaiʻi Pidgin, 
Make it possible to analyze/ compare 2 different word cloud data.

Optional:
Make Word cloud viewing page animated
Make It possible to compare multiple word clouds 3+,









===================== IDEAS SECTION =====================

Layout style inspiration/ references:
https://store.steampowered.com/, https://www.youtube.com/, 

Home page presents the cloud data first, prioritizing content 





These are just layout sketches, color schemes can be applied later
Considerations for Mobile view use: Make left side bar collapsable


Database structure: How will we store our data to the db and what do we need to store to implement certain features
	User table: *same as template users
ID (int), 
email (string @unique), 
password (string), 
role (user or admin)
accessiblewc (int[]) 
# unique ids of word cloud data that the user can access even if that data is private, always contains the user’s created wc data
		bookmarkedwc (int[]) 
	WordCloud table:
		owner (string), 
unique entry id(int), 
word frequency data (json), 
word list(string[]), 
language(string), 
upload datetime (int formatted as yyyymmddhhmmss to make it easier to sort), 
text citation source (string), 
text author (string),
dataset description (string), 
tags (string[]), 
sharing type (int: public, private, restricted, or unpublished), 
views counter (int), # Total views, used for sorting by all-time popularity
recent views counter (int[]) # used to figure out which ones are trending
cloud data title (string) 
editors (string[]) # who can modify the word cloud data
bookmarks (int)
	Posts: * similar to digits note
		owner (string), 
unique entry id(int), 
cloud data id (int), 
timestamp (DateTime @default(now()))
description (string)
comments (Comment[])
	Comments: * same as digits note model
		owner (string), 
unique entry id (int), 
		post unique id (int),
		comment (string),
		timestamp (DateTime @default(now()))


		
Core features:
Users copy-paste plain text into a text field that will run the WordCloud generation function, that generates a json object with “word” keys assigned with their corresponding “frequency” values or the number of times they show up in the text source.
User can edit generated cloud data by:
Removing certain words from the data set, such as “the”, “a”, “is”, “it”, “they”, and other words that may appear in high frequencies but don’t contribute to the qualitative analysis.
Merging word frequencies: Ie: “word” and “words” can be merged by adding the frequency of 1 to the other then removing it ->[ word: 1002, words: 15 => word: 1017 ]
When publishing (setting to public) for the first time, publication date is set
