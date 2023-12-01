# Paste below content¬
FROM ubuntu:latest AS BUILD_IMAGE
RUN apt-get update && apt-get -y install wget unzip
WORKDIR /tmp
RUN wget --progress=dot:mega https://www.tooplate.com/zip-templates/2128_tween_agency.zip && unzip 2128_tween_agency.zip
WORKDIR /tmp/2128_tween_agency
RUN tar -czf tween.tgz ./* && mv tween.tgz /root/tween.tgz
FROM ubuntu:latest
LABEL "project"="Marketing"
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y install apache2 git wget
COPY --from=BUILD_IMAGE /root/tween.tgz /var/www/html/
WORKDIR /var/www/html/ && tar xzf tween.tgz
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
VOLUME /var/log/apache2
EXPOSE 80
