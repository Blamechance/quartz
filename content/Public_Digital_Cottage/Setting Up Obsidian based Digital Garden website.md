---
title: Setting Up Obsidian-based Digital Garden website
date: 2023-07-18T16:14
tags:
- obsidian
- quartz
---

In looking for a simpler static site generator, I stumbled upon the following video: 

* [Publishing your Vault Online With Quartz](https://brandonkboswell.com/blog/Publishing-your-Obsidian-Vault-Online-with-Quartz/) - [Brandon Boswell](https://brandonkboswell.com/blog/Publishing-your-Obsidian-Vault-Online-with-Quartz/)
* I found this method to have a few too many gaps in instruction to replicate his home brewed solution. 

I decided instead to stand on the shoulders of [jackyzha0](https://github.com/jackyzha0/quartz) 's incredible Quartz repo as the touchstone instead, and adapt my solution from there. 

In the event it's useful for others, here are the steps I took to get it all going.

---

## Linux (ubuntu) installation:

Firstly, fork and clone the following repo locally:
`https://github.com/jackyzha0/quartz`

### 1. Install Hugo:

Quartz runs on top of Hugo, so we'll need to independently install it. For me, this was on linux, but hugo has documentation for installation on other OS's too.

````
sudo snap install hugo
````

### 2. Install `Hugo-obsidian` + Go dependencies, if required:

1. Install go if not already installed on system.
   
   * Make sure go version is (>= 1.16).
   * [Go installation page](https://gohugo.io/installation/)
2. Initialise a new go module for project, using github repo URL. e.g

````
go mod init github.com/Blamechance/blamechance.github.io
````

If you experience path issues, indicated by `command not found` errors:

	a. Confirm where GO installed itself (normally in `~/[user]` folder).
	
	b. Edit or create `.bash_profile` file in user directory.
	
	c. Add the following line to the file, e.g:

```
export PATH="$HOME/go/bin:$PATH"
```

Run the following to load the edited config to current shell (you might need to restart your app if operating terminal in something like vscode for same effect):
`source ~/.bash_profile`

3. Install `hugo-obsidian` to enable backlink conversion, for local site live previewing:

   a. Get the modules required:
   
   ````
   go get github.com/jackyzha0/hugo-obsidian
   ````
   
   b. Install from repo:
   
   ````
   go get go install github.com/jackyzha0/hugo-obsidian
   ````
   
   c. Test with:
   
   ````
   hugo-obsidian version
   ````

3. To run, navigate to the folder where quartz was cloned and run:
   
   ````
   make serve
   ````

### 3. Copy obsidian/markdown files to quartz

1. Navigate to the desired obsidian folder to upload.
   
   * I set up my vault to have a `public` and a `private` folder. 
   * My workflow for now will involve working in obsidian, and logically considering the `public` folder the space where I move notes I want to share. 
   * All notes/posts will be edited and created through the obsidian -> export process, with the only elements needing editing within an IDE being the index file, CSS, html etc. 
1. Copy the folder into the `content` folder in your quartz directory.

1. That's it! Run `make serve` to view your website locally, and push to your github repo to host it on [Github pages](https://quartz.jzhao.xyz/notes/hosting/).

#### Automating export:
Here's a quick and dirty bash script to clears the repo's copy of the vault and index files, to copy in the current ones from the obsidian vault location. 

Automating this process means the creation process of posts is simple:
1. Write/edit posts and index file as notes in obsidian
2. Run `make serve` to host local render of website. 
3. Run script in terminal to update the browser render live. 
4. To post, push on git! 

Feel free to adapt if useful.

```bash
#!/bin/bash


SOURCE_PATH=~/path/to/source
DESTINATION_PATH=~/path/to/destination

# Delete all files in the target export folder - public_digital_garden is the folder that i've placed all my obsidian notes in (both in my vault and the quartz folder). Adapt for your folder name. 

rm "$DESTINATION_PATH"/Public_Digital_Garden/*
rm "$DESTINATION_PATH"/_index.md

# Copy index file and public folder from obsidian vault to export folder for git pushing
cp -r "$SOURCE_PATH"/Public_Digital_Garden "$DESTINATION_PATH"/
cp "$SOURCE_PATH"/_index.md "$DESTINATION_PATH"/
```
---
#### References: 
Resources:
* https://github.com/jackyzha0/quartz
* https://quartz.jzhao.xyz/notes/hosting/
* https://quartz.jzhao.xyz/notes/troubleshooting/
* https://quartz.jzhao.xyz/notes/config/
