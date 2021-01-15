# Wordpress by OQILA

This is a little customized version of Wordpress. This is intented for professional development.

### Features:

1. It comes with pre-installed Advanced Custom Field, Classic Editor plugins,
1. Default theme is WP Bootstrap Starter, which is empty and great start point for development custom theme,
1. Local environment related configurations are moved to seperate file and ignored by Git,
1. No installation steps are required. Just import database and run!
1. Missing `.htaccess` and `.gitignore` files are provided,
1. No site address changing via phpMyAdmin each time you move to other domen.

**Note** All terminal examples are shown in Linux. If you are using Windows then do it in its way.

## Installation:

1. Download and unzip [this repo](https://github.com/oqila/wordpress/archive/master.zip) into the folder where you want to install your new project. Alternatively you can clone:
```
   git clone https://github.com/oqila/wordpress.git
```
1. Change `wordpress` folder name to your new project name, e.g. `ados.uz`
```
    mv wordpress ados.uz
```
1. Create empty database for project via phpMyAdmin with `utf8mb4_general_ci` collation
1. Import `*project-folder*/install/db.sql` backup sql file into the newly created database
1. [Linux only] Set proper file permissions with prepared script
```
    ./*project-folder*/install/secure_site_dir *project-folder*/
```
1. Now to go project folder and duplicate `wp-config-local.php.dist` with name `wp-config-local.php`
```
    cd *project-folder*/
    cp wp-config-local.php.dist wp-config-local.php
```
1. Edit database and site url parameters
1. Optionally create empty file with name `DEBUG` at `*project-folder*`. This enables wordpress debug mode which is helpful during development process
1. Your project should have its own remote git repo, so set it
```
    git remote set-url origin https://*remote url*.git
```

## Apache configuration on Linux

1. Create file `/etc/apache2/sites-available/*project name*.conf`
1. Put this on that file
```
    <VirtualHost *:80>
        ServerName *your-domain*.loc
        ServerAlias www.*your-domain*.loc

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/vhosts/*project folder*

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
```
Here `DocumentRoot` may be different at your machine
1. `sudo a2ensite *project name*`
1. `sudo service apache2 restart`
1. Add following to `/etc/hosts` file
```
    127.0.1.1   *your-domain*.loc
```

## Working with upstream for getting latest changes

Read more about [upstream](https://www.atlassian.com/git/tutorials/git-forks-and-upstreams)

Let's see remote
`git remote -v`

Let's add upstream
`git remote add upstream https://github.com/oqila/wordpress.git`

Let's download latest changes
`git fetch upstream`

Now time to merge changes
```
git checkout master
git merge upstream/master
```

If you have merge conflict use `git mergetool`