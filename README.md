# Open Litter Map Deployment
OLM Deployment repo is used to store all files needed to run an environment on a server.

## Used commands

### WEB
#cd /home/phummelen/openlittermap/littertagger
docker build --rm -t phummelen/hero-web:latest -f deployment/web-dev.dockerfile .

docker run --rm -it -p 9000:9000 phummelen/hero-web:latest

### DOCS
cd /home/phummelen/openlittermap/olm-documentation
docker build --rm -t phummelen/hero-docs:latest -f deploy/build/dockerfile .

### MTA
cd /home/phummelen/openlittermap/olm-deploy
docker build --rm -t phummelen/olm-mta:latest -f mta/Dockerfile .

### Initialize the database

Get dummy data: php artisan migrate:fresh --seed
Get migration action done: php artisan migrate

