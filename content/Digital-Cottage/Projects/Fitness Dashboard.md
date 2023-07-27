---
title: "Fitness Dashboard"
date: 2023-07-26T22:56
enableToc: false
tags:
- fitness
- flask
- python
- HTML
- CSS
---
## Concept: 
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

