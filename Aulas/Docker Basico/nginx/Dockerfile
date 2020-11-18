FROM nginx:latest
LABEL MAINTAINER 'CRONOS2277'
RUN useradd www
USER www
VOLUME /log
WORKDIR /usr/share/nginx/html/
COPY *.* /usr/share/nginx/html/
EXPOSE 8080