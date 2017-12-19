Some scrapy spider are scheduled by crontab. this project fixed crontab running in docker.
Based on vimagic/scrapyd, mysql connection and ALSQLchema for python is added.
Spider code is loaded in volume, after docker-compose runs.
You may start your spider code in crontab file.
