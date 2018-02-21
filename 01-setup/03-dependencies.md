# Dependencies

## RVM
RVM is short for **Ruby Version Manager**. RVM makes it easy to install and manage different versions of Ruby.

To install RVM, first verify that you have `curl` installed by typing `$ curl --version` into your terminal.  If you don't have it installed, type `sudo apt-get install curl`.

Install RVM by running this command

	\curl -L https://get.rvm.io | bash -s stable


Close and reopen your terminal window. Verify that RVM was installed correctly by running this command

	rvm | head -n 1

## Ruby 2.2.3
Install Ruby 2.2.3 by typing this into your terminal. This might take a while.

	rvm install 2.2.3
	
Verify that Ruby was installed (You may have to run "source .bash_profile" to build the path)
	
	ruby -v
	
## Gems
[RubyGems](https://rubygems.org/) is a package manager for Ruby that provides a standard format for sharing programs and libraries in small packages called **gems**. The `gem` command is used to build, upload, download, and install RubyGem packages.<sup>[1](http://stackoverflow.com/questions/5233924/what-is-a-ruby-gem)</sup>

The **Gemfile** is a list of all the gems you want to include in your Rails project. It is used in conjunction with `bundler` to install, update, and remove your gems.

Install `bundler` with this command

	gem install bundler


## MySQL

MySQL is a Database Management System which we use to organize and store our data. Installing and configuring MySQL can be a little tricky, so double check the installation commands before running them. Don't worry if you get an error though, many people on the internet probably have had a similar problem.

_Note_:
MySQL can use large amounts of your memory


#### Mac
These directions are for Mac OS X **10.11 El Capitan**. To check which version of OS X you have, click the apple logo in the top left of the screen and select 'about'.

Install MySQL using Homebrew. The default user for MySQL is the `root` user with no password

	brew install mysql

These commands will start MySQL on login, and load MySQL

	ln -sfv /usr/local/opt/mysql/*plist ~/Library/LaunchAgents
	launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist

#### Ubuntu
Install MySQL on Ubuntu by running these two commands

	sudo apt-get update
	sudo apt-get install mysql-server
	
You will be prompted to select a root password during installation. Pick one that you will remember.

[Next &raquo; Configuration](/01-setup/04-configuration.md)
