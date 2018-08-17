# README file for Project Logs Analysis
## Udacity Full Stack Nanodegree
For more info see this [link](https://classroom.udacity.com/nanodegrees/nd004/parts/51200cee-6bb3-4b55-b469-7d4dd9ad7765/modules/c57b57d4-29a8-4c5f-9bb8-5d53df3e48f4/lessons/bc938915-0f7e-4550-a48f-82241ab649e3/concepts/079be127-2d22-4c62-91a8-aa031e760eb0).

Before running the code, please make sure you create following two Views in the "news" database:
## VIEW path_slug:

CREATE VIEW path_slug AS	
SELECT DISTINCT log.path as path, articles.slug as slug 
FROM log, articles
WHERE position(articles.slug in log.path) > 0

and 

## VIEW article_stat:
CREATE VIEW article_stat AS
SELECT articles.id as id, count(log.path) as count
FROM log, path_slug, articles
WHERE articles.slug = path_slug.slug AND
path_slug.path = log.path
GROUP BY articles.id


Once two views are created, you may proceed with execution:
Before running the code, please make sure you create following two Views in the "news" database:

### vagrant@vagrant:/vagrant/logs-analysis$ python3 logs-analysis.py
