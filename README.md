<h1>Install-PHP-mysql-Valet-in-Ubuntu</h1>
<h2>
Here you are advised to set up your ubuntu environment to run a PHP or laravel projects with Nginx server. You can seemlink your mysql server with PHPMyAdmin to run it in simple way by Valet.
</h2>
<hr>
<br>

# Before Running Any Command You Need To Run
~~~
sudo apt-get update && sudo apt-get upgrade
~~~

or
~~~
sudo apt update && sudo apt upgrade
~~~

# Now Install Curl
~~~
sudo apt install curl
~~~

# Now Check Curl Version
~~~
curl --version
~~~

# Install Nginx Server for PHP dependecies
~~~
sudo apt install nginx
~~~

# Install PHP with FPM
~~~
sudo apt install php-fpm
~~~
it will install php 7.4 in your ubuntu and you are good to go

# Now Check PHP version
~~~
php -v
~~~

# run this again
~~~
sudo apt-get update
~~~

# Install Nginx repository
~~~
sudo add-apt-repository ppa:ondrej/nginx
~~~

# To check the status of PHP that it has collabrate properly with Ngnix repository
~~~
sudo systemctl status php8.1-fpm
~~~

# Now Restart Nginx
~~~
sudo nginx -t
~~~
then
~~~
sudo systemctl restart nginx
~~~

# Install Network Manager Now
~~~
sudo apt-get install network-manager libnss3-tools jq xsel
~~~

# Install PHP Extensions
~~~
sudo apt-get install php-zip && sudo apt-get install php-mbstring && sudo apt-get install php-curl
~~~
It will automatically detect your version and do its own work

# run this again
~~~
sudo apt-get update
~~~

# Install Composer
~~~
curl -sS https://getcomposer.org/installer -o composer-setup.php
~~~

# Set Composer Address

~~~
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
~~~

# Now Check Composer version
~~~
composer
~~~

# run this again
~~~
sudo apt-get update
~~~

# Install valet
~~~
composer global require cpriego/valet-linux
~~~
then
~~~
test -d /.composer && bash /.composer/vendor/bin/valet install || bash ~/.config/composer/vendor/bin/valet install
~~~

# Command for update valet version
~~~
composer global update
~~~
then
~~~
valet install
~~~

# run this again
~~~
sudo apt-get update
~~~

# Install MySQL Server
~~~
sudo apt install mysql-server -y
~~~

# Adjusting mysql Authentication
~~~
sudo mysql
~~~
then
~~~
SELECT user,authentication_string,plugin,host FROM mysql.user;
~~~
then
~~~
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
~~~
then
~~~
FLUSH PRIVILEGES;
~~~
now exit by
~~~
exit;
~~~

# run this again
~~~
sudo apt-get update
~~~

# Install phpmyadmin
~~~
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
~~~

if you face any difficulties follow the below link
https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-20-04

# Symlink phpmyadmin With MySQL Server
Now You have to go to your C Drive & open the Terminal and run this
~~~
sudo chmod -R 777 /var/www
~~~
This will give Permission to Symlink now come back to root terminal & run this
~~~
ln -s /usr/share/phpmyadmin /var/www/phpmyadmin
~~~
Then
~~~
sudo chmod -R 777 /var/www/phpmyadmin
~~~

# run this again
~~~
sudo apt-get update
~~~

# Install Node JS
~~~
sudo apt install nodejs
~~~
then check nodejs version
~~~
node -v
~~~

# Install NPM
~~~
sudo apt install npm
~~~
then
~~~
sudo apt-get install --reinstall nodejs-legacy     # fix /usr/bin/node
~~~

<h2>You are good to go, Now develop your web application in your ubuntu by Using Laravel & PHP....</h2>




# Serving Sites by Valet
Once Valet is installed, you’re ready to start serving sites. Valet provides two commands to help you serve your Laravel sites: park and link.

<h3>The Park Command</h3>

Create a new directory on your machine by running something like
~~~
mkdir ~/folder-name
~~~
 Next,
~~~ 
cd ~/folder-name
~~~
and run
~~~
valet park
~~~
This command will register your current working directory as a path that Valet should search for folder-name.
Next, create a new Laravel site within this directory: 
Open http://folder-name.test in your browser.
That’s all there is to it. Now, any Laravel project you create within your “parked” directory will automatically be served using the http://folder-name.test convention.

<h3>The link Command</h3>

The link command may also be used to serve your Laravel sites. This command is useful if you want to serve a single site in a directory and not the entire directory.

To use the command, navigate to one of your projects, open your terminal and run
~~~
 valet link
~~~
Valet will create a symbolic link in ~/.valet/Sites which points to your current working directory.
After running the link command, you can access the site in your browser at http://app-name.test.
To see a listing of all of your linked directories, run this command
~~~
valet links
~~~
You may use this to destroy the symbolic link.
~~~
valet unlink app-name
~~~

