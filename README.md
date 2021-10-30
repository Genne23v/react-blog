# Web Server for Blog Site

\*This is from LinkedIn Learning React: Creating and Hosting a Full-stack Site.
This express web server uses local MongoDB storage for blog articles, user comments and upvotes. React front-end blog site is HERE.

#

## AWS Hosting

1. Go to AWS Management Console. Then select EC@ in All services
2. Create Instance -> Launch Instance
3. Select Amazon Linux 2 AMI
4. Click 'Review and Launch'
5. Click 'Launch'
6. 'Select an existing key pair or create a new key pair' pop-up display. Then select 'Create a new key pair' in a dropdown list.
7. Enter Kay pair name and download the key pair. Then click 'Launch Instance'.
8. Move the downloaded key to ~/.ssh (Create one if not existing)
9. Go back to AWS console. Move to EC2 -> Running Instances.
10. Select an instance that is just created. Copy 'Public DNS'.
11. Update key file permission

```
chmod 400 ~/.ssh/my-blog-key.pem
```

12. Enter below command on the terminal to access to AWS terminal

```
ssh -i ~/.ssh/my-blog-key.pem ec2-user@<copied-public-DNS>
```

#

## Setting Up an AWS Instance

1. In AWS terminal, enter below to set up Git

```
sudo yum install git
```

2. Install node version manager with below commands

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

3. Activate nvm

```
. ~/.nvm/nvm.sh
```

4. Use nvm to install the latest version of Node.js

```
nvm install <version-used-for-my-project>
```

5. Get the latest npm packages

```
npm install -g npm@latest
```

6. Set up MongoDB

```
sudo nano /etc/yum.repos.d/mongodb-org-5.0.repo
```

7. Add below to the file

```
[mongodb-org-5.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2/mongodb-org/5.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-5.0.asc

```

8. Install MongoDB

```
sudo yum install -y mongodb-org

sudo service mongod start
```

9. Add some initial data to MongoDB

#

## Running Full-stack App on AWS

1. Copy GitHub repo on AWS

```
git clone <http-github-repo>

npm install

npm install -g forever

forever start -c "npm start" .
```

2. You can check running repo with <code>forever list</code>

```
forever list
```

3. Map port to 80

```
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 8000
```

4. Go back to AWS browser console and select 'Security Group'
5. Select the instance to create security group
6. Click 'Inbound' tab and click EDIT
7. Select Type - HTTP, Source - Anywhere
8. Copy public DNS on main console and paste it to browser address bar to access
9. Now app is running!
