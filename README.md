# AmCat Docker

# Installation

## Requirements
* Docker and Docker Compose installed

## Running

### (Optionally) Build the docker containers first 
```
docker-compose -p amcat build --force-rm
```
### Start the services
```
docker-compose -p amcat up -d
```


### Populate the database and set the elasticsearch mapping
```
docker-compose -p amcat run --no-deps amcat python -m amcat.manage migrate
```

You can now open the website at 192.168.99.100:8000 (or your docker ip address) and login using the credentials amcat/amcat. Don't forget to change this password.

### Create a super user

```
docker-compose -p amcat run --no-deps amcat python -m amcat.manage createsuperuser
```

### Create a worker

```
docker-compose -p amcat run --no-deps -e DJANGO_SETTINGS_MODULE=settings amcat celery -A amcat.amcatcelery worker -l INFO -Q amcat --broker amqp://guest:guest@rabbitmq//
```

or as a deamon

```
docker-compose -p amcat run -d --no-deps -e DJANGO_SETTINGS_MODULE=settings amcat celery -A amcat.amcatcelery worker -l INFO -Q amcat --broker amqp://guest:guest@rabbitmq//
```

## Get content

### Scraping content
#### List available scrapers
```
docker-compose -p amcat run --no-deps amcat-scraping python -m amcatscraping.scrape list
```
#### Start a scraper
```
docker-compose -p amcat run --no-deps amcat-scraping python -m amcatscraping.scrape run fok.nl
```

## Notes

### Login into the AmCAT Docker container

This may be useful for fixing errors or changing configuration.
```
docker exec -it amcat_amcat-scraping_1 bash
```
