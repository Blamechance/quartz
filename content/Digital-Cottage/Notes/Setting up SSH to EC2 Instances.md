---
title: Setting up SSH to EC2 Instances
date: 2024-02-11T14:15
enableToc: false
tags:
  - SSH
  - AWS
---

# For existing/running instances:
1. Navigate to "Key Pairs" in the AWS EC2 console menu.
2. Create Key pair - name it something memorable or it will default to `id_rsa.pem`. Check `.pem` when prompted on the key file format. 
	- The browser will automatically download the private key file. 
3. On Mac/linux, use the following command:
	`ssh-keygen -y`
	- Then provide the path to the private key file when prompted. 
	- The public key will be output. 
4. Connect to the existing instance using `EC2 Instance Connect`. 
5. Navigate to the `.ssh` folder, and open the `.ssh/authorized_keys` file on the instance.
6. Paste the public key information from your new key pair underneath the existing public key information. Save the file.
7. Disconnect from your instance, and test that you can connect to your instance using the new private key file.
	- From ubuntu, you can run the `ssh` command with the `-i` flag to specify the private key. e.g:
	`ssh -i your-key-ssh.pem ec2-user@13.0.0.1`

> [!Info]
>If you're replacing an existing key pair, connect to your instance and delete the public key information for the original key pair from the `.ssh/authorized_keys` file.

# For new instances: 


# Setting up SFTP
After a bunch of trial attempts, Filezilla wouldn't authenticate properly for me (configured keys, paths, permissions and auth methods several times). Ended up just using SFTP through terminal as suggested [here](https://stackoverflow.com/a/46725492).

## Steps:
Connect with the EC2 Instance with:

```
sftp -i "path/to/key.pem" ec2-user@ec2-54-212-34-84.us-west-2.compute.amazonaws.com
```

### Downloading files / dirs

To download `path/to/source/file.txt` and `path/to/source/dir`:

```
lcd ~/Desktop
cd path/to/source
get file.txt
get -r dir
```

### Uploading files / dirs

To upload `localpath/to/source/file.txt` and `~/localpath/to/source/dir` to `remotepath/to/dest`:

```
lcd localpath/to/source
cd remotepath/to/dest
put file.txt
put -r dir
```

#### Resources: 
- https://stackoverflow.com/questions/45198768/how-to-find-aws-keypair-public-key
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html#having-ec2-create-your-key-pair
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/replacing-key-pair.html
- https://www.cyberciti.biz/faq/how-to-install-ssh-on-ubuntu-linux-using-apt-get/
