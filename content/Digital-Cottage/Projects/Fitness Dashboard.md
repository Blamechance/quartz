---
title: "Fitness Dashboard"
date: 2023-07-26T22:56
enableToc: false
tags:
- Flask
- Python
- HTML
- CSS
---
# Concept: 
My friends and I are big fans of a simple gym-tracking app that serves to replace a simple notebook and pen, called "FitNotes". 

The app allows us to easily keep track of our gym routine, rep schemes during workouts, historical logs of previous workouts etc. We've also recently came into the habit of using this, and checking in with each other at the end of every month to share progress and other notes on training. 

The concept for this project is to create a web app that takes the exported CSV data from the FitNotes app, and uses it generate a fun dashboard that will extend the app's usecase, and enhances those conversations. 

Some key ideas: 
- Make the monthly check-in process easy by simply uploading the CSV data. 
- Provide more robust data analytics/graphs based on the CSV data, than what is available within the app. 
- Support for tracking of bodyweight related data points as well. 
- Potentially integrate with a discord webhook, for frictionless user experience within the same platform that our discussion tend to take place.
	- Output after check-in could also be sent to the discord channel as a webhook response, to share with everyone else. 

# Links:
The github repository is [here](https://github.com/Blamechance/fitness-dashboard). 
A copy of the `README.md` is [[Digital-Cottage/Notes/Fitness Dashboard README|here.]]

Here's a quick video walk-through: 
![Youtube Link.](https://youtu.be/Np4lORlm-Y0)

# Development/Feature Backlog: 

## Misc. Dev Backlog items: 

| Task                                                                        | Status |
| --------------------------------------------------------------------------- | ------ |
| Implement TDEE calculator                                                   | ⬜      |
| Add feature to allow users to delete their account/data                     | ⬜      |
| Add a page to display user data across all accounts                         |        |
| Integrate a dev pipeline to allow live build/update to site of new features |        |
Table Key: ⬜ Not Started, ⚙️ In Progress, 🚧 On Hold, ✅ Completed

# Project Tracking:

## Ver 1.0 - Creating Flask App Basic Functionality:
The target for this iteration is to have a functional working proof of concept. 

- ✅  Create the flask web app structure, complete with HTML pages/layouts. 
- ✅  Apply Bootstrap + CSS for out the box presentability. 
- ✅   Find minimal libraries to represent CSV data and graphs/charts
	- (tabulator + charts.js). 
- ✅  Implement a user account system. 
- ✅  Implement the first iteration of the app:
	- ✅  Allow user uploads for server processing. 
	- ✅   Create basic functionality of processing fitnotes export files for JSON output, utilising `pandas` for `.csv` parsing. 
	- ✅  Charts.js rendering from JSON. 
	- ✅  tabulator rendering from JSON. 


## Ver 1.1 - Hosting The App Online:
The Tl;DR of it is that I went with a AWS Free Tier Ubuntu 20.04 instance, hosting it on my domain managed with CloudFlare. 

It's accessible [here](https://fitness-dashboard.tcao.dev/login)!

- [[Digital-Cottage/Notes/Setting Up AWS Sub-Account Structure For Projects|Setting Up AWS Sub-Account Structure For Projects]]
- [[Digital-Cottage/Notes/Serving a Flask Web App on AWS using Gunicorn And Nginx|Serving a Flask Web App on AWS using Gunicorn And Nginx]]

### Notes And Considerations Over Architecture: 
#### Unwanted Traffic: 
Currently, I do not utilise any services that might accrue extra charges in the result of unintended/DDOS traffic. The users who I would be sharing this to, and who would actually use it can be counted on one hand. 

**Action:**
- Implement cloudwatch alarms that track resource utilisations. 
- Set a reminder to swap from T3.Micro to a spot instance after close to a year lol. 
#### Potential Attacks / Exploitation:
I've designed the app to be relatively stateless; this means all user data can be quickly produced anytime they submit their Fitnotes file (no functionality for changes to data server side -- all changes should be made within the app). 

**Action:**
- If ever choosing to implement real data such as emails etc, utilise better controls such as RDS instead of the SQLite db. 
- Don't implement any form of user *download* functionality, just in case it's ever compromised. Keep the project as a way to receive and represent user given data.  
- I don't think it's worth justifying paying for **NAT Gateways** or **NLBs** yet, so I'll do the less tasteful decision to host my EC2 instance in a public subnet for now. 
	- In future, once I've got more apps to show I can obsfucate them all behind a single NLB -- especially when security is a higher concern. Currently though, **there's no real user data to be compromised**
	- Something like the following... 
		![[Digital-Cottage/Projects/attachments/aws.drawio.png]]
#### Considering Serverless:
A serverless design with Lambda was considered, but current app design makes use of session data for users functionality. Also, cold starts to lambda might make the experience lacklustre. 
# V3: 
⬜ Integrate the app's CI with gitlab pipeline, so further updates will build to the live site. 


