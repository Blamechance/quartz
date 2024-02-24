---
title: Setting up Flask Web App serving from EC2 Instance
date: 2024-02-07T19:36
enableToc: false
tags:
  - Flask
  - AWS
---
# Preface: 
Firstly, I highly recommend setting up a virtual environment in your main project's directory to allow reliable reproduction of all required dependencies. 
# Configuration Steps:

1. **Ensure you have created a `requirements.txt`  file from the local directory.**
	- This can alternatively be done with other environment tools like `venv` and `virutalenv`, but I've used `pipenv`. 
2. **Create ubuntu EC2 instance.** 
	- If looking to stay in free tier, choose the instance type highlighted as such (currently T2 Micro). 
	- I chose Ubuntu Server 20.04 LTS. 
3. **Set-up SSH/SFTP, if not yet already configured.** 
	- I generally use Filezilla for SFTP. 
	- Strictly speaking this can be optional, as you can use EC2 Instance Connect in your browser, and `git` instead of SFTP. 
1. **Install `Python3`, `pip`, `Apache2` and `mod_wsgi` modules.** 
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
	- [[Digital-Cottage/Notes/Private/Troubleshooting Fitness Dashboard Ubuntu Module Compatibility|Private/Troubleshooting Fitness Dashboard Ubuntu Module Compatibility]]
```sh

sudo apt install pipenv
sudo pipenv install
```


### Resources:
[How to Deploy a Flask App to Linux (Apache and WSGI)](https://www.youtube.com/watch?v=w0QDAg85Oow) - luke peters
[Deploying a Flask Application via the Apache Server](https://www.opensourceforu.com/2023/03/deploying-a-flask-application-via-the-apache-server/)- opensourceforu
[Deploying Flask Application on Ubuntu (Apache+WSGI)](https://tecadmin.net/deploying-flask-application-on-ubuntu-apache-wsgi/) - tecaadmin
[How to Install Apache Web Server on Amazon Linux 2](https://dev.to/mkabumattar/how-to-install-apache-web-server-on-amazon-linux-2-31l) - dev.to
[Flask documentation to `mod_wsgi` configuration](https://flask.palletsprojects.com/en/2.3.x/deploying/mod_wsgi/) - Flask
[Creating a Flask Web Server in EC2 on the AWS Free Tier from scratch! (Gunicorn)](https://www.youtube.com/watch?v=z5XiVh6v4uI) - Vincent Stevenson
[How to Deploy Flask with Gunicorn and Nginx (on Ubuntu)](https://www.youtube.com/watch?v=KWIIPKbdxD0)- Tony Teaches Tech
