---
# 1. Add tags
# 2. Add title

# Note: Avoid using 
# i. Special characters (like dashes and speech marks) for note title. 
# ii. Ending in puncutations for  yaml title.  

# Backlinks will populate with waypoint page, to MOC. 

title: "Setting up AWS sub-account structure for projects"
date: 2023-11-24T09:24
enableToc: false
tags:
- AWS
---

>[!note] 
> AWS is shifting towards a system of IAM Identity Center (previously AWS SSO) federation and permission sets as recommended best practice, for setting up console/access keys. 
> This provides temporary credentials for access for a role, instead of for IAM users. 
> [Read more here](https://docs.aws.amazon.com/cli/latest/userguide/sso-configure-profile-token.html). 




When creating a new AWS account, there are several best practices that should be applied before you start building: 
1. Configure MFA. 
2. Create a new account, to retire the root account from admin usage. 
3. Create an organisation unit per project. 
4. Apply IAM users, roles and apply least-privilege principle to account access -- i.e create separate accounts for separate projects etc. 
5. If multiple accounts are created, make sure to utilise consolidated billing, and set-up SCPs to again apply least-privilege to accounts. 
6. Set up billing alarms for any used resources, especially if trying to stick to free tier. 

Doing this manually and without the assistance of tools such as Terraform, CDK, Control Tower etc. is tedious, so if you're looking to repeat the creation of these environments often, I would look into those tools. 

# Steps:
## 1. Configure MFA
**Root account:**
1. Click on the account name on the top-left, then "Security Credentials". 
2. Under MFA, click "Assign MFA Device". 
3. Configure preferred MFA method.
4. Sign out and Sign back in to verify. 

**Subsequent Users:**
1. Head to the IAM Identity Center and enable the service with AWS Organisations. 
2. In the subsequent window, click on "Configure multi-factor authentication (MFA)".
3. Review the settings before saving changes. Recommend to check:
	- "*Require them to register an MFA device at sign in*"
4. Sign out of the account and sign back in to set-up MFA on root account. 

## 2. Create a new IAM User admin account
Create an admin account to perform administrator duties, aside from those that require the management account. After this account is made, **we mostly retire the management account**. 

**Creating Administrator Group:**
1. In the **IAM Console**, click on Groups -> Create Group on the left-hand panel. 
2. Assign a group name and check the box on the provided permission policy "*AdministratorAccess*" (should be the top most policy in that table). 
3. Click **Create Group** at the bottom. 

**Creating Administrative user**:
This is the account to use from now on, unless organisation changes need to be made. 
1. Staying in the **IAM Console** Click on **Users -> Add User.**
2. Set a username and password - good practice is to have that user set a new password on sign-in. Click next. 
3. Add that user to the previously created **administrator group**, and click next. 
4.  Review the configuration and create user. Make sure to save the provided URL here for signing in.
5. Sign in using the link, and repeat setting up MFA. 

## 3. Creating an OU/sub-account for different projects
In essence, there should be a single management account serving to consolidate all sub-accounts. Under that, there will be a projects OU, with further sub-OUs to house each specific project, such as below: 

![[Digital-Cottage/Notes/Private/attachments/AWS Projects Accounts.png|Private/attachments/AWS Projects Accounts.png]]

1. Navigate to AWS Organisations and click on **"Add an AWS account**". 
2. Create a new account filling in a separate email address
	- Tip: If you've got a gmail account, you can make use of their aliasing feature to utilise a single email for multiple user accounts. 
	- e.g useremail@gmail.com can be used again with useremail+whateveryouwantsuffix@gmail.com. 
3. Open another incognito window and log into that newly created account, using the "root account" sign in options. 
4. ==Set-up MFA for this new project account!==
5. Navigate back to AWS Organizations, and check on the "**Root"** folder. 
6. Click on the "Actions" button top-right, and create new organisational unit (I named mine "projects").
7. Click on that newly created OU, and create another one with the specific project name, e.g above "fitness-dashboard". 
8. Add new AWS accounts to that specific project OU, following best practice of a Development and Prod account. 

## 4. Creating admin roles and worker roles for subsequent accounts:
For those newly created project specific accounts, we need to follow the same process of protecting the root AWS account, opting for an admin account instead. 
1. Follow step 2 within each of the DEV/PROD accounts, to create administrator IAM users. 
	- Enable MFA!
2. Create one extra IAM user for each of the accounts also, to represent the "non-administrative worker". 
	- ==Don't attach this IAM user to the administrators group!==
	- e.g `fitness-dashboard-worker`. 

## 5. Creating IAM Roles for worker access to services
Best practice is to only provide "workers" with the specific access they require, to do their job.
This is best applied through assigning access permissions to **IAM Roles**, based on the **IAM Group** the user belongs to. 
There are many ways to do this, but here's a simple way using in-line policies (process is made through the admin account):

1. Head to **IAM -> Roles -> Create Role**.
2. Check box for "Trusted Entity Type", for **"AWS Account**", and "Require MFA".
3. Select the required policies, such as "*AmazonEC2FullAccess*". 
4. Set a role name and create. 
5. Navigate to the worker user in **IAM -> Users**. 
6. Click "Add Permissions" under the "Permissions" tab. 
7. Switch the view to `JSON` and add the ARNs to each of the new roles like so:
	- This allows the user to assume the specified roles. 
```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Allow",
			"Action": "sts:AssumeRole",
			"Resource": [
				"arn:aws:iam::[your_acc_no]:role/EC2-S3-full-access",
				"arn:aws:iam::[your_acc_no]:role/VPC_R53_fullaccess"
			]
		}
	]
}
```

8. Save changes! 
	- Note the ARN lines down for next steps in enabling switching roles. 

### Switching Roles: 
The worker user should have access to assume both roles now, and this can conveniently done through:
1. In the top-right menu, and click  "Switch Role". 
2. Click "Switch Role" again. 
3. Enter the account number and, per it's inclusion in the ARN. 
4. Enter the role name under "Role". 
5. The display name and colour are up to your preference. 
6. Click switch role. Switched roles will be shown in the top-right menu for future convenience. 
![[Digital-Cottage/Notes/Private/attachments/Setting up AWS sub-account structure for projects.png|Private/attachments/Setting up AWS sub-account structure for projects.png]]






---
##### Resources: 
- https://docs.aws.amazonA.com/singlesignon/latest/userguide/mfa-configure.html
- https://docs.aws.amazon.com/streams/latest/dev/setting-up.html
- https://www.youtube.com/watch?v=zVJnenaD3U8
- https://mim-armand.medium.com/steps-to-create-an-aws-sub-accounts-free-tier-2268b17c9f7
- https://docs.aws.amazon.com/organizations/latest/userguide/orgs_tutorials_basic.html
- https://dev.to/aws-heroes/setting-up-a-multi-account-aws-environment-1h67
- https://www.reddit.com/r/aws/comments/109776f/how_should_individual_developers_access_devprod/
