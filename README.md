# Open Litter Map Deployment
OLM Deployment repo is used to store all files needed to run an environment on a server.

## Used commands

### WEB
cd /home/phummelen/openlittermap
docker build --rm -t olm/web:latest -f olm-deploy/web/Dockerfile .

docker run --rm -it -p 8000:8000 olm/web:latest

### DOCS
cd /home/phummelen/openlittermap
docker build --rm -t olm/docs:latest -f olm-deploy/docs/Dockerfile .
