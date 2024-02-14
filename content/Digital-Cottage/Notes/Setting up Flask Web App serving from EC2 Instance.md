---
title: Setting up Flask Web App serving from EC2 Instance
date: 2024-02-07T19:36
enableToc: false
tags:
  - Flask
  - AWS
---
>[!note]
>Will pull notes from [[Digital-Cottage/Notes/Private/Fitness Dashboard Dev v2|Fitness Dashboard Dev v2|Private/Fitness Dashboard Dev v2|Fitness Dashboard Dev v2]] to populate this. 
# Configuration Steps:
1. **In your local/github repo where the flask app is hosted, ensure you have created a [[Digital-Cottage/Notes/pipenv|pipfile]].** 
	- This can alternatively be done with other environment tools like `venv` and `virutalenv`, but i've used `pipenv`. 
2. **Create ubuntu EC2 instance.** 
	- If looking to stay in free tier, choose the instance type highlighted as such (currently T2 Micro). 
	- I chose Ubuntu Server 20.04 LTS. 
3. **Set-up SSH/SFTP, if not yet already configured.** 
4. **Install `Python3`, `pip`, `Apache2` and `mod_wsgi` modules.** 
```py
sudo apt-get install python3 python3-pip python3-venv 
sudo apt-get install apache2 libapache2-mod-wsgi-py3
```
5. **Upload your Flask files to the server, in the apache folder directory `/var/www`.** 
	Make sure that you have `sudo` admin access to allow upload here, in whichever method you are using. 
	- You can do this through your SFTP connection (filezilla, sftp in terminal).
	- Alternatively, if you have uploaded your flask app to github, you can `git clone` to the respective directory also.
6. **In the project's created folder, create a `logs` folder.**
	- `/var/www/project-name/logs`
7. **Using the pipfile , install the virtual environment**
	- [[Digital-Cottage/Notes/Fitness Dashboard Ubuntu Module Compatibility|Fitness Dashboard Ubuntu Module Compatibility]]
```sh
sudo pipenv install
```


## Working Space:
Errors in creating environment:
```sh
Installing dependencies from Pipfile.lock (292158)…
An error occurred while installing dbus-python==1.2.18! Will try again.
An error occurred while installing pycairo==1.23.0; python_version >= '3.7'! Will try again.
An error occurred while installing pygobject==3.42.1; python_version >= '3.6' and python_version < '4'! Will try again.
An error occurred while installing pyinotify==0.9.6! Will try again.
An error occurred while installing systemd-python==234! Will try again.

```
Crux of the issue is that these dependencies expect previous python version, though project currently runs python 3.8.10.
- Installing python3.6 is proving annoying - have managed to update libcairo/pycairo, so going to try and solve each dependency that is lagging behind. 
Attempt fix:
```sh
# Following is all run after installing latest python3 and pip
sudo apt-get install python3 python3-pip python3-venv 

# installing cairo before pycairo due to error:
#   Command ['pkg-config', '--print-errors', '--exists', 'cairo >= 1.15.10']
sudo apt-get install libcairo2-dev # installed 1.16, Pipfile line: libcairo2-dev = "==1.16" 
pip install pycairo
sudo apt-get install python-gobject-2-dev 
sudo apt install libgirepository1.0-dev
sudo apt-get install libsystemd-dev
pip install dbus-python
sudo apt-get install libdbus-1-dev libdbus-glib-1-dev
```

**Current state:** Environment will activate, but modules aren't installed on checking... 

### Resources:
[How to Deploy a Flask App to Linux (Apache and WSGI)](https://www.youtube.com/watch?v=w0QDAg85Oow) - luke peters
[Deploying a Flask Application via the Apache Server](https://www.opensourceforu.com/2023/03/deploying-a-flask-application-via-the-apache-server/)- opensourceforu
[Deploying Flask Application on Ubuntu (Apache+WSGI)](https://tecadmin.net/deploying-flask-application-on-ubuntu-apache-wsgi/) - tecaadmin
[How to Install Apache Web Server on Amazon Linux 2](https://dev.to/mkabumattar/how-to-install-apache-web-server-on-amazon-linux-2-31l) - dev.to
[Flask documentation to `mod_wsgi` configuration](https://flask.palletsprojects.com/en/2.3.x/deploying/mod_wsgi/) - Flask
