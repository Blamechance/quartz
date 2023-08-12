---
# 1. Add tags
# 2. Add title

# Note: Avoid using 
# i. Special characters (like dashes and speech marks) for note title. 
# ii. Ending in puncutations for  yaml title.  

# Backlinks will populate with waypoint page, to MOC. 

title: "Achieving AWS SA - Associate (SAA-C03) Certification"
date: 2023-08-12T12:27
enableToc: true
tags:
- AWS
- Learning-journal
---

[View my badge!](https://www.credly.com/badges/c3452de8-7ff6-41a5-a3e4-0a88af63e75d/public_url)

**Certified**: 11th Aug 2023. 



![[Digital-Cottage/Notes/attachments/Achieving AWS SA - Associate (SAA-C03) Certification.png]]


## Thoughts on Content: 
Generally, all cloud service offerings are based on existing technologies that customers would host themselves and that many are already familiar with. Based on this, I found it useful to: 

- Frame learning with a perspective of [[Digital-Cottage/Resonance Journal/Focusing Your Unconscious Mind - Learn Hard Concepts Intuitively (And Forever)|"inventing"]] the solutions myself. 
	- I did this as I progressed through the content - linking it to tech I'm already familiar with, and other ones that I wasn't yet.

- Alternate between top-down and bottom up learning. 
	- Lead this based on curiosity and naturally arising questions. Doing so would often walk me to "ah-ha!" moments. 

- Similar of my experience working at AWS, documentation of services is **robust** and should be used as the first contact sources of truth.
	- Diving into the FAQs/documentation would often lead to any context or answers I was missing. 

These things helped me understand concepts on a deeper level, particularly with:
1. What it does
2. Why it was developed; and 
3. Where it's value/role slots into cloud architecture design. 

## Thoughts on the Exam:
It shouldn't be overlooked that this is an exam-based certificate. Unavoidable priorities include: 

- Familiarising with common *patterns* and *anti-patterns.* 
	- *e.g*  Discerning between the ELB, DB and storage offerings for their respective use cases. 

- Get comfortable with breaking down question structure efficiently. 
	- I found it useful to read from the questions bottom up - I felt it allowed better identification of the important details, when reading through the fluff. 

- Make use of free tier and tinker within the AWS console, to anchor learned content. 
	- I made little notes along the way for ways I can make use of services within personal projects. 

- It was also quite interesting to learn the concepts and relate it to the server hardware's design/architecture that I work with, making guesses in how the HWeng teams translated requirements into the design. 
	- Internally, we use different code names for hardware to disassociate server from service (as well as tight controls on information), so my guess is as good as any but ...
	- It's fun to theorise on elements such as whether aurora storage is hosted on S3 or EBS based hardware. 



## Napkin Scratch AWS Project ideas:
While working through the content, I had fun letting my mind wander on potential uses for the services within future project ideas. 

- Use an S3 bucket with [[Digital-Cottage/Projects/Fitness Dashboard|Fitness Dashboard]] to store backup/archives of either the user’s input spreadsheets, or output JSON files. 

- Include proof of concept (and probably overdesigned) elements of high availability, fault-tolerance and disaster recovery for web-app, just to better familiarise with the concepts.

- Host an OOB error page with S3 static hosting and R53 DNS fail-over, for both [[Digital-Cottage/Projects/Fitness Dashboard|Fitness Dashboard]] and this [[_index|Digital Cottage website]]. 
	- Potentially covered by free tier of AWS Shield Standard? 
	
- Experiment with various ways to break up the current monolithic design of projects to:
	- Dockerised containers. 
	- Serverless architecture, running functions out of lambda. 

- Host webapp projects in "self-healing" auto-scaling groups, out of spot instances to ensure high availability. 
