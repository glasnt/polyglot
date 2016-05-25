# polyglot
Code for my Becoming a Polyglot talk

In this repository are examples in several languages of a basic API in a common framework for that language.  They all use the same mongodb backend, and all use the same single page HTML application.

All of them run at http://localhost:8080

The following paths work in each environment:
* /api/quotes => quote list
* /api/quotes/random => random quote
* / => hello world from the framework
* /demo => Single page HTML application

# Setup

## Mongo
You will need to have mongodb installed and running.  Installation info for the major platforms is at https://docs.mongodb.org/manual/installation/

To insert the information from the quoteid.json file to get your DB started, use the following command:

`mongoimport --collection quotes --file ../data/quoteid.json --type json --jsonArray`

# PHP

```
php composer.phar install 
pecl install mongo
php -S 0.0.0.0:8080 -t ./public/ ./public/index.php
```

# Python

`cd python; pip install -r requirements.txt; python flask-server.py`

# Node
For express:
`cd node; npm install; node express-server.js`

For hapi:
`cd node; npm install; node hapi-server.js`

# Ruby
`cd ruby; gem install bundler; bundle install; ruby sinatra-server.rb`

# Perl
`sudo cpan -i -f Dancer Dancer::Plugin::CRUD JSON MongoDB; perl dancer-server.pl`

# Docker setup
You can skip all of the setup instructions above and use the docker container if you like.
First, install docker from http://www.docker.com/toolkit
Next:
  * Start the docker shortcut utility, note the IP address it gives
  * `docker run -i -t -p 8080:8080 synedra/polyglot`
  * `/etc/init.d/mongodb start`
  * `mongoimport --collection quotes --file ../data/quoteid.json --type json --jsonArray`
  * run the startup command for whichever language you like
  * The server will be running on http://{docker-ip}:8080


# Cloud 9

Alternatively, you can use Cloud 9 (https://c9.io) to setup a cloud-based containerised environment. 

 * Setup a new workspace based on the 'PHP/Apache' image, cloning from this repo
 * Setup and run mongo within a new c9 terminal tab based on https://community.c9.io/t/setting-up-mongodb/1717, plus installing required packages for the c9 environment:

```
cd php
php composer.phar install 
cd ..
sudo apt-get install php5 php5-dev libapache2-mod-php5 apache2-threaded-dev php-pear php5-mongo -y
wget http://pecl.php.net/get/mongo
sudo pecl install mongo
echo 'mongod --bind_ip=$IP --dbpath=data --nojournal --rest "$@"' > mongod
chmod a+x mongod
./mongod
```
 * In a new tab: load the mongo data from the `mongoimport` command above
 * follow the Setup instructions for the PHP, Python, Node, Ruby and Perl instructions as usual.
