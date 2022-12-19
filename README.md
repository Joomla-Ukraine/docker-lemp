# docker-lemp

## Docker Commands

**Build without using cache**

`docker-compose build --no-cache`

**Start Container** 

`docker-compose up -d`

## Docker complete data (ex: container and volume etc) and rebuild

**Step 1:** Stop docker container (remove containers) 

`docker-compose down`

**Step 2:** Prune docker data 

`docker system prune -a`

**Step 3:** Prune docker images 

`docker image prune`

**Step 4:** Prune docker volumes 

`docker volume prune`

**Step 5:** Rebuild without using cache 

`docker-compose build --no-cache`

**Step 6:** Start Container 

`docker-compose up -d`
