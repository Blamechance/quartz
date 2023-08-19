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

## Development: 
The intention is for a simple full-stack web-app consisting of Python, HTML/CSS and some lightweight Javascript.

It's a project with simple intention, but should spur a lot of learning along the way -- more than anything though, I'm excited to create a complete product with real use-case. 

I'm currently plugging away at the working prototype [here](https://github.com/Blamechance/fitness-dashboard)!

### Project Tracking:

<br>

| Task                                                                                          |     Status     | Description                                                                                                                           |
|:--------------------------------------------------------------------------------------------- |:--------------:| ------------------------------------------------------------------------------------------------------------------------------------- |
| Add user log-in functionality                                                                 | ⚪ Not Started |                                                                                                                                       |
| Add better storage/archive of processed data                                                  | ⚪ Not Started | Could back up provided CSV, processed JSON etc.. as long as it's saved somewhere other than local to server and time stamped to user. |
| Break server side functions into [Clean Code](/Digital-Cottage/Notes/Clean%20Code) principles | ⚪ Not Started |                                                                                                                                       |
| Host project on AWS                                                                           |   🚧 On Hold   | Acquired AWS:SA Associate certificate. Completing project before migrating to cloud.                                                                                |

<br>

| Task                                                          |     Status     | Description                                |
|:------------------------------------------------------------- |:--------------:| ------------------------------------------ |
| Create logic functions to process CSV to JSON (training data) | ⚙️ In Progress |                                            |
| Create logic functions to process CSV to JSON (weight data)   | ✅ Completed   |                                            |
| Client side asynchronous CSV submit button                    | ✅ Completed   |                                            |
| athlete/user page with skeleton structure for populating      | ✅ Completed   |                             |
| Chart.js Graphs for plotting data                             | ✅ Completed   | Created custom logic to scale graph axis from current epoch time, would've been easier to use Bolton library... |
| Nav bar                                                       | ✅ Completed   | Adapted bootstrap.                         |
| HTML Layout Skeletons                                         | ✅ Completed   |         |
| Set-up repo + flask environment                               | ✅ Completed   | Need to test in different / cloned repo environments.                                            |

Table Key: ⚪ Not Started, ⚙️ In Progress, 🚧 On Hold, ✅ Completed 


