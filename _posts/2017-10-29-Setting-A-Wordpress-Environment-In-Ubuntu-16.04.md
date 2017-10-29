---
  layout: post
  title: Setting A Wordpress Environment In Ubuntu 16.04
  tags: 
  categories: Wordpress
  permalink: /blog/:title.html
---

Quick Installation in your terminal. Execute by order.

{% highlight shell %}
sudo apt-get install apache2
sudo apt-get install libapache2-mod-php7.0 php7.0-mysql php7.0-curl php7.0-json
sudo apt-get install mysql-server
mysql -u root
Create database wordpress;
create user 'woprdpress'@'localhost' identified by 'MyWPPassword';
GRANT ALL PRIVILEGES ON wordpress. * TO 'wordpress'@'localhost';
exit
cd /var/www/html/
sudo apt-get install wget
sudo wget https://wordpress.org/latest.tar.gz
sudo tar xvfz latest.tar.gz
ls -la
sudo chown www-data.www-data -R wordpress/
sudo service apache2 restart
{% endhighlight%}

You should now be able to access [http://localhost/wordpress](http://localhost/wordress) and continue.