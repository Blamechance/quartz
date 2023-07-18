
---
title: "Setting Up Obsidian-based Digital Garden website"
date: 2023-07-18T16:14
tags:
- obsidian
- quartz
---
  
### First attempt:
On first attempt, I was looking to replicate the following

- [Publishing your Vault Online With Quartz](https://brandonkboswell.com/blog/Publishing-your-Obsidian-Vault-Online-with-Quartz/)
- I found this method to have a few too many gaps in instruction to replicate his home brewed solution for selective upload of vault files.


### Final solution
I ended up deciding to stand on the shoulders of [jackyzha0](https://github.com/jackyzha0/quartz) for the time being and use his incredible Quartz Repo. 
- Currently, this means manually copying in the "public" folder of my obsidian vault, each time I want to upload.
- Eventually I plan to automate this with my own cron-job based script.

Resources:
- https://github.com/jackyzha0/quartz
- https://quartz.jzhao.xyz/notes/hosting/
- https://quartz.jzhao.xyz/notes/troubleshooting/
- https://quartz.jzhao.xyz/notes/config/

  

---

## Linux (ubuntu) installation:

In the event it's useful for others, here are the steps I took to get it all going.

Firstly, fork and clone the following repo locally:
`https://github.com/jackyzha0/quartz`


### 1. Install Hugo:

Quartz runs on top of Hugo, so we'll need to independently install it. For me, this was on linux, but hugo has documentation for installation on other OS's too.

```
sudo snap install hugo
```

  

### 2. Install `Hugo-obsidian` + Go dependencies, if required:

1. Install go if not already installed on system.
	- Make sure go version is (>= 1.16).
	- [Go installation page](https://gohugo.io/installation/)

2. Initialise a new go module for project, using github repo URL. e.g
```
go mod init github.com/Blamechance/blamechance.github.io
```


If you experience path issues, indicated by `command not found` errors:

1. Confirm where go installed it's folder (normally in `~/[user]` folder).

2. Edit or create `.bash_profile` file in user directory.

3. Add the following line to the file, e.g:
```
export PATH="$HOME/go/bin:$PATH"
```

Run the following to load the edited config to current shell (you might need to restart your app if operating terminal in something like vscode for same effect):
	`source ~/.bash_profile`

3. Install `hugo-obsidian` to enable backlink conversion, for local site live previewing:
	a. Get the modules required:
	```
	go get github.com/jackyzha0/hugo-obsidian
	```
	b. Install from repo:
	```
	go get go install github.com/jackyzha0/hugo-obsidian
	```
	c. Test with:
	```
	hugo-obsidian version
	```

4. To run, navigate to the folder where quartz was cloned and run:
	```
	make serve
	```

### 3. Copy obsidian/markdown files to quartz
1. Navigate to the desired obsidian folder to upload.
	- I set up my vault to have a `public` and a `private` folder. 
	- My workflow for now will involve working in obsidian, and logically considering the `public` folder the space where I move notes I want to share. 
	- All notes/posts will be edited and created through the obsidian -> export process, with the only elements needing editing within an IDE being the index file, CSS, html etc. 

2. Copy the folder into the `content` folder in your quartz directory.

3. That's it! Run `make serve` to view your website locally, and push to your github repo to host it on [Github pages](https://quartz.jzhao.xyz/notes/hosting/). 
