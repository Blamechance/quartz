---
title: Serving a Flask Web App on AWS using Gunicorn And Nginx
date: 2024-02-07T19:36
enableToc: true
tags:
  - Flask
  - AWS
  - Cloudflare
---
# Summary:
In this example, I've hosted a flask web app on a personal domain, accessible to the public. 
- The web server is hosted on an AWS Free Tier instance. 
- I've used **Gunicorn** here as it makes Python web-serving much easier. 
	- Gunicorn allows web server requests to interact with the flask app. 
- Nginx is the web server of choice here
- I used **Cloudflare** as my domain registrar, providing added benefit of free SSL certificates. 


# Creating Instance and Installing Dependencies:

1. **Ensure you have created a `requirements.txt`  file from the local directory.**
	- This can alternatively be done with other environment tools like `venv` and `virutalenv`, but I've used `pipenv`. 
	- [[Digital-Cottage/Notes/Setting Up A Virtual Env For Development|Setting Up A Virtual Env For Development]]
1. **Create Ubuntu EC2 instance.** 
	- If looking to stay in free tier, choose the instance type highlighted as such (currently T2 Micro). 
	- I chose Ubuntu Server 20.04 LTS. 
2. **Set-up SSH/SFTP, if not yet already configured.** 
	- I generally use Filezilla for SFTP. 
	- Strictly speaking this can be optional, as you can use EC2 Instance Connect in your browser, and `git` instead of SFTP. 
3. **Install `Python3`, `pip`, `Apache2` and `mod_wsgi` modules.** 
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
7. **Using Requirements.txt file, install all required dependencies**
	```sh
	sudo pip install -r requirements.txt 
	```

# Gunicorn:
1. Test all your required dependencies are installed properly. Run flask locally to make sure it's all working as it should. 
	```sh
	# If your instance network settings are allowing public access, this should allow the app to be accessible from http://[your-instance-ip]:5000
	flask run --host=0.0.0.0
	```


*WIP - from here on*

2. Install Gunicorn:
```sh
pip install gunicorn
```
3. Create `wsgi.py` file in same directory as your `app.py` (main flask app code)  file. 
4. Test the `wsgi` and gunicorn are running properly with the following command, testing public access again.
	```sh
	gunicorn --bind 0.0.0.0:5000 wsgi:app
	```
5. Create a `systemd` service to allow web serving to recover in the event of service interruptions/intermittent host states. 

# Nginx
1. Install Nginx
2. Create `.conf` file to any custom domains. 
3. Ensure permissions to flask app dir is accessible by the user, by which Gunicorn will be run. 
### Resources:
- [How to Deploy a Flask App to Linux (Apache and WSGI)](https://www.youtube.com/watch?v=w0QDAg85Oow) - luke peters
- [Deploying a Flask Application via the Apache Server](https://www.opensourceforu.com/2023/03/deploying-a-flask-application-via-the-apache-server/)- opensourceforu
- [Deploying Flask Application on Ubuntu (Apache+WSGI)](https://tecadmin.net/deploying-flask-application-on-ubuntu-apache-wsgi/) - tecaadmin
- [How to Install Apache Web Server on Amazon Linux 2](https://dev.to/mkabumattar/how-to-install-apache-web-server-on-amazon-linux-2-31l) - dev.to
- [Flask documentation to `mod_wsgi` configuration](https://flask.palletsprojects.com/en/2.3.x/deploying/mod_wsgi/) - Flask
- [Creating a Flask Web Server in EC2 on the AWS Free Tier from scratch! (Gunicorn)](https://www.youtube.com/watch?v=z5XiVh6v4uI) - Vincent Stevenson
- [How to Deploy Flask with Gunicorn and Nginx (on Ubuntu)](https://www.youtube.com/watch?v=KWIIPKbdxD0)- Tony Teaches Tech
