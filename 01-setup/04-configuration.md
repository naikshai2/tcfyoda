# Configuration

At this point, you should have installed all the tools you need (except Rails!). In this section we will set up the actual codebase so that you can start developing. This involves configuring GitHub, your MySQL database, and finally theCourseForum project.

## Git
#### Set up SSH keys
Secure Shell (SSH) is a network protocol that let's you perform work on a remote machine. Generating SSH keys and adding them to GitHub will make development easier.

1. Type this command into your terminal. It creates a new ssh key, using your github email address

	
		$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
		
2. When prompted to "Enter a file in which to save the key", just press Enter. This accepts the default file location

		Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
		
3. When prompted for a password, you can either enter a password or press enter

		Enter passphrase (empty for no passphrase): [Type a passphrase or enter]
		Enter same passphrase again: [Type passphrase again or enter again]
		
4. Make sure the ssh-agent is running

		$ eval "$(ssh-agent -s)"
		
5. Add the new key to your local ssh-agent

		$ ssh-add ~/.ssh/id_rsa
		
6. Copy the public key to your clipboard. Navigate to `/Users/you/.ssh/` and copy the contents of `id_rsa.pub` to your clipboard. Go to github.com, click on your profile, settings, ssh keys. Click on "SSH and GPG Keys" then "New SSH Key". Paste in your key and save your changes.

7. Verify that you set up ssh correctly

		$ ssh -v git@github.com
		...
		...
		...
		"Hi User! You've successfully authenticated, but GitHub does not provide shell access."

#### Clone theCourseForum Repository
Now that ssh is set up, clone theCourseForum repository to your computer. This gives you access to the same code with which everyone else is working.

1. Go to https://github.com/thecourseforum/theCourseForum

2. Click on "Clone or download", then make sure that it is ssh

3. Copy the ssh path and open your terminal

4. Navigate to where you want to clone the repository, and run this command

		$ git clone git@github.com:thecourseforum/theCourseForum.git
		
## MySQL

<img src="http://i.imgur.com/zYt1N8b.gif">

This part notoriously sucks. But do it enough times and you'll see that there is only so much that can go wrong with MySQL.


Right now, your MySQL is empty. We need to add theCourseForum database to MySQL so that you can load the project.

1. Go to **http://phpmyadmin.thecourseforum.com/** and ask someone for the password

2. Once you're logged in, expand **_thecourseforum_** tab on the left

3. Export the `thecourseforum_development` and `thecourseforum_production` databases as shown in the picture below
<img src="http://i.imgur.com/iFSkE8K.png">

4. These next directions assume the databases are in your `Downloads` folder

5. Log into your MySQL database
		
		$ mysql -u root -p 
		[Enter your password]

6. List all of your current databases

		mysql> show databases; 

7. If you don't already have `thecourseforum_development` and/or `thecourseforum_production` databases, skip this step. Otherwise, drop these databases.

		mysql> drop database thecourseforum_development; 
		mysql> drop database thecourseforum_production; 

8. Create new databases for each of the ones you downloaded

		mysql> create database thecourseforum_development; 
		mysql> create database thecourseforum_production; 

9. Import the downloaded `thecourseforum_development.sql` file into your new database

		mysql> use thecourseforum_development; 
**Note**: Some team members will tell you to source production instead of development. Sourcing development is what should be done, but if there are problems later on in your setup come back to this step.
		
		mysql> source ~/Downloads/thecourseforum_development.sql 
		
10. Do the same for `thecourseforum_production.sql`

		mysql> use thecourseforum_production; 
		mysql> source ~/Downloads/thecourseforum_production.sql 
		
11. Type `exit` or `ctrl + d` to close MySQL
		

## Configuring the Repository

In your terminal or text editor, open the cloned directory for theCourseForum. If you're using a text editor like Atom or Sublime, it is easier to open a new project.

#### Bundle
Install the needed gems in your Gemfile. The bundle command will take a while to run because it has to install **Rails 4.2.4**

		$ cd theCourseForum/
		$ bundle install
		
#### `database.yml`
Database configuration file

		$ cp config/database.yml.skel config/database.yml
		
		Add your MySQL password to the password fields in database.yml
		Verify that the socket field has a correct path!!!
		
#### `devise.rb`
Authentication gem

		$ cp config/initializers/devise.rb.example config/initializers/devise.rb

#### `secret_token.rb`
Super secrety

		$ touch config/initializers/secret_token.rb

		Add TheCourseForum::Application.config.secret_key_base = "othersecretkey1234"
		
#### `application.yml`
More config stuff

		$ cp config/application.yml.example config/application.yml

		Needed for global environment variables from figaro gem
		

## Rails Server
After all this setup, you're ready to run the server and see the website on your localhost. Navigate to theCourseForum directory and enter (and remember) this command

	$ rails s

Output should look something like this

	=> Booting Thin
	=> Rails 4.2.4 application starting in development on http://localhost:3000
	=> Run `rails server -h` for more startup options
	=> Ctrl-C to shutdown server
	>> Thin web server (v1.5.1 codename Straight Razor)
	>> Maximum connections set to 1024
	>> Listening on localhost:3000, CTRL+C to stop
	
	
That's it. Now continue with the instructional guides in this repo to practice using your new dev environment!

<img src="http://i.imgur.com/QS7x8TC.gif">


		
