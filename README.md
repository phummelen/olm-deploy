# Open Litter Map Deployment
OLM Deployment repo is used to store all files needed to run an environment on a server.

## Used commands
docker build --rm -t olm/app:latest -f olm-deploy/api/Dockerfile .

cd /home/phummelen/openlittermap/openlittermap-web
docker build --rm -t olm/app:latest -f ../olm-deploy/api/Dockerfile2 .

docker run --rm -it -p 8000:8000 olm/app:latest