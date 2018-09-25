# Project: Logs Analysis @ Udacity Full Stack Nanodegree

This is a reporting project for a newspaper site, with the database behind it. The exact task is to generate following three reports:

1. The most popular three articles of all time
2. The most popular article authors of all time
3. Days when more than 1% of requests lead to errors

## Included files
a) logs-analysis.py - python code
b) Vagrantfile - Vagrant configuration file
c) README.md - this file
d) output.txt - expected run output

## Dependencies
Python 3.6.6 [download](https://www.python.org/downloads/release/python-366/)
VirtualBox Version 5.2.16 [download](https://download.virtualbox.org/virtualbox/5.2.16/)
Vagrant 2.1.2: Use this [link] (https://releases.hashicorp.com/vagrant/2.1.2/) to download it and attached Vagrantfile to configoure it.

## Setup and run instructions:

1. Download database from this [link](https://d17h27t6h515a5.cloudfront.net/topher/2016/August/57b5f748_newsdata/newsdata.zip)

2. Start virtual machine with command
### vagrant up

3. Connect to virtial machine with command:
### vagrant ssh

4. Move to the working directory:
### vagrant@vagrant:/vagrant/logs-analysis$ cd /vagrant

5. Load data with command:
### vagrant@vagrant:/vagrant/logs-analysis$ psql -d news -f newsdata.sql
The database includes following three tables:
authors table - includes information about the authors of articles.
articles table - includes the articles themselves.
log table - includes one entry for each time a user has accessed the site.

6. in PSQL execute following SQL command to create a helper view path_slug:
### CREATE VIEW path_slug AS	
### SELECT DISTINCT log.path as path, articles.slug as slug 
### FROM log, articles
### WHERE position(articles.slug in log.path) > 0

7. in PSQL execute following SQL command to create a helper view article_stat:
### CREATE VIEW article_stat AS
### SELECT articles.id as id, count(log.path) as count
### FROM log, path_slug, articles
### WHERE articles.slug = path_slug.slug AND
### path_slug.path = log.path
### GROUP BY articles.id

8. Run the project code by executing following command on operting system prompt:
### vagrant@vagrant:/vagrant/logs-analysis$ python3 logs-analysis.py
