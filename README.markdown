# cappress ![Project status](http://stillmaintained.com/jadb/cappress.png)

Looking to deploy a [Wordpress](http://wordpress.org) website? Cappress extends [Capistrano](http://capify.org), removing the *rails-ism*, replacing them by more *wp-ish* ones.

*Cloned from [Capcake](http://github.com/jadb/capcake)*

## Installation

If you don't have Capistrano and/or Cappress already installed (basically, just the 1st time):

	# gem install capistrano
	# gem install cappress -s http://gemcutter.org

For every application you'll want to deploy:

	# cd /path/to/app && capify .

This will create the following files in your project (don't forget to commit them!):

	capfile
	config/deploy.rb

Prepend your config/deploy.rb with the following lines:

	require 'rubygems'
	require 'cappress'

And make sure you start cappress on the last line of that same file:

	cappress

You should then be able to proceed as you usually would. To familiarize yourself with the now modified list of tasks, you can get a full list with:

	$ cap -T

## Configuration

Before continuing, some changes to config/deploy.rb are necessary. First, your project's name:

	set :application, "your_app_name"

Next, setting up the Git repository (make sure it's accessible by both your local machine and server your are deploying to):

	set :repository, "git@domain.com:path/to/repo"

Now, to deploy from Git, and by following [GitHub's suggestion](http://github.com/guides/deploying-with-capistrano) (they must know what they are talking about), add a user (defaults to *deployer* by cappress's recipe) to your server(s) just for deployments. In this example, I will be using SSH keys instead of getting a Git password prompt. Local user's SSH key must be added to *deployer*'s ~/.ssh/authorized_keys for this to work as described. 

	ssh_options[:forward_agent] = true

We need to tell it where to deploy, using what methods:

	server "www.domain.tld", :app, :db, :primary => true

And finally, some CakePHP related settings (if omitted, Cappress will NOT handle deploying Wordpress):

	set :wp_branch, ""

You can change the default values for the following variables also:

	set :wp_branch, "1.2"
	set :wp_path, "/path/to"
	set :user, "your_username"
	set :branch, "tag"

## Deployment

The first time you are deploying, you need to run:

	# cap deploy:setup

That should create on your server the following directory structure:

	[deploy_to]
	[deploy_to]/releases
	[deploy_to]/shared
	[deploy_to]/shared/wordpress
	[deploy_to]/shared/system
	[deploy_to]/shared/uploads

Finally, deploy:

	# cap deploy

Which will change the directory structure to become:

	[deploy_to]
	[deploy_to]/current -> [deploy_to]/releases/20091013001122
	[deploy_to]/releases
	[deploy_to]/releases/20091013001122
	[deploy_to]/releases/20091013001122/system -> [deploy_to]/shared/system
	[deploy_to]/releases/20091013001122/wp-content/uploads -> [deploy_to]/shared/uploads
	[deploy_to]/shared
	[deploy_to]/shared/system
	[deploy_to]/shared/uploads

## Patches & Features

* Fork
* Mod, fix
* Test - this is important, so it's not unintentionally broken
* Commit - do not mess with license, todo, version, etc. (if you do change any, make them into commits of their own that I can ignore when I pull)
* Pull request - bonus point for topic branches

## Bugs & Feedback

http://github.com/jadb/cappress/issues