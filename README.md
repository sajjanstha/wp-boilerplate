# WordPress boilerplate with Git and Composer, and an Improved folder structure


## Why WordPress as a Dependency?
By treating WordPress itself as a dependency you can make the structure of your Git repo more modular and clean.

## Improved Folder Structure
    │
    ├── public/                    # nginx will point to this folder as starting point
    │   ├── wp-content/            # Our themes, plugin & uploads are moved here
    │   ├── wp/                    # Our subdirectory install location for WordPress (not stored in Git repo)
    │   ├── .htaccess              # Only needed if using Apache
    │   ├── index.php              # Entry point for our Website
    │   └── wp-config.php          # will hold any “global” config information and then load the correct “environment” config file as required
    └── .gitignore                 # ignores .idea, vendor, core wordpress, specified plugins and themes
    └── composer.json              # Composer dependency defined here
    └── local-config.sample.php    # copy this file to local-config.php or production-config.php depending upon environment

## Installation Steps
This repo is meant to be used as a boilerplate for your new Wordpress Project. Submit Pull Request only if you want to contribute improving this boilerplate.
* Download the zip by visiting url (Do not clone): `https://github.com/pagevamp/smart-worpress-setup/archive/staging.zip`
* Extract zip and Goto project folder: `cd [foldername]`
* Setup your Own git repo: `git init && git remote add origin git@github.com:pagevamp/<project-name>.git"`
* Push your first commit: `git commit -am "wordpress boilerplate" && git push -u origin master`
* Create new database for your wordpress
* Configure your wordpress : `cp local-config.sample.php local-config.php` (`cp local-config.sample.php production-config.php` for production), then change the config variables to match your settings
* Put your database credentials in local-config.php or production-config.php file
* Initialize docker: `sudo docker-compose up -d`
* Open bash terminal inside container: `sudo docker exec -it <demo-site.pv> /bin/bash`
* Install dependencies: `composer install`
* Add your preferred local domain name to hosts file (for example, demo-site.local) : `sudo vim /etc/hosts`
* Visit your project url (demo-site.local) in web browser and complete your Wordpress Installation
* That's it!!
* Enjoy building your Wordpress themes with Ease

## Add Plugin as composer dependency
The WordPress Packagist(https://wpackagist.org) site helps us out here by mirroring the WordPress plugin and theme directories as a Composer repository. 
We can specify which plugins and themes we want to install in our composer.json file. Suppose you want to install 'Show Current Template' plugin then
run this command inside your docker container `compose require wpackagist-plugin/show-current-template`

## Caveat
Your WordPress admin will now always have "/wp" in the URL. To remove it from the front site make sure the following options are set 
in your options table in the database:
* siteurl: http://example.com/wp (with /wp)
* home: http://example.com (without /wp)

Reference:
* https://deliciousbrains.com/install-wordpress-subdirectory-composer-git-submodule/


