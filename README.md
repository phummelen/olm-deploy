# Open Litter Map Deployment
OLM Deployment repo is used to store all files needed to run an environment on a server.

## Used commands

### WEB
cd /home/phummelen/openlittermap
docker build --rm -t olm/web:latest -f olm-deploy/web/Dockerfile .

docker run --rm -it -p 9000:9000 olm/web:latest

### DOCS
cd /home/phummelen/openlittermap
docker build --rm -t olm/docs:latest -f olm-deploy/docs/Dockerfile .

### MTA
cd /home/phummelen/openlittermap
docker build --rm -t olm/mta:latest -f olm-deploy/mta/Dockerfile .


### Initialize the database

Get dummy data: php artisan migrate:fresh --seed
Get migration action done: php artisan migrate

