FROM squidfunk/mkdocs-material as build-docs

COPY ./olm-documentation/documentation /documentation

WORKDIR /documentation

RUN mkdocs build -f config/en/mkdocs.yml
RUN mkdocs build -f config/fr/mkdocs.yml
RUN mkdocs build -f config/nl/mkdocs.yml
RUN mkdocs build -f config/de/mkdocs.yml

#--- Second part
FROM nginx:stable-alpine-slim


# Copy nginx config
COPY ./olm-documentation/deploy/config/nginx.conf /etc/nginx/conf.d/default.conf

# Copy project
COPY --from=build-docs /documentation/generated /usr/share/nginx/html

# Set port
EXPOSE 80

## switch to non-root user
## not needed to mention, is done in the container by itself
#CMD bash