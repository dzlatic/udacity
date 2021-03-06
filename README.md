# Project: Logs Analysis @ Udacity Full Stack Nanodegree

This is a reporting project for a newspaper site, with the database behind it. The exact task is to generate following three reports:

1. The most popular three articles of all time
2. The most popular article authors of all time
3. Days when more than 1% of requests lead to errors

## Included files


| File | Comment |
| ------ | ------ |
| logs-analysis.py | python code |
| Vagrantfile | Vagrant configuration file |
| README.md | this file |
| output.txt | expected run output |


## Dependencies

| Software | Version | Download |
| ------ | ------ | ------ |
| Python | 3.6.6 | [link](https://www.python.org/downloads/release/python-366/) |
| VirtualBox | 5.2.16 | [link](https://download.virtualbox.org/virtualbox/5.2.16/) |
| Vagrant | 2.1.2 | [link](https://releases.hashicorp.com/vagrant/2.1.2/) |


## Setup and run instructions:

1. Download database from this [link](https://d17h27t6h515a5.cloudfront.net/topher/2016/August/57b5f748_newsdata/newsdata.zip)

2. Start virtual machine with command:
    #### vagrant up

3. Connect to virtial machine with command:
    #### vagrant ssh

4. Move to the working directory:
    #### vagrant@vagrant:/vagrant/logs-analysis$ cd /vagrant

5. Load data with command:
    #### vagrant@vagrant:/vagrant/logs-analysis$ psql -d news -f newsdata.sql

6. Check the database includes following three tables:

| Table | Content |
| ------ | ------ | 
| authors | information about the authors of articles |
| articles | the news articles |
| log | includes one entry for each time a user has accessed the site |

7. In PSQL prompt execute following SQL command to create the first helper view:
    #### CREATE VIEW path_slug AS	
    #### SELECT DISTINCT log.path as path, articles.slug as slug 
    #### FROM log, articles
    #### WHERE position(articles.slug in log.path) > 0

8. In PSQL prompt execute following SQL command to create a second helper view:
    #### CREATE VIEW article_stat AS
    #### SELECT articles.id as id, count(log.path) as count
    #### FROM log, path_slug, articles
    #### WHERE articles.slug = path_slug.slug AND
    #### path_slug.path = log.path
    #### GROUP BY articles.id

9. Run the project code by executing following command on operting system prompt:
    #### vagrant@vagrant:/vagrant/logs-analysis$ python3 logs-analysis.py

10. Compare the output with the content of output.txt file.
