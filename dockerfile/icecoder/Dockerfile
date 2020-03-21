FROM php:7.2-apache
WORKDIR /root/
RUN apt-get update && apt-get install -y unzip
ADD https://icecoder.net/download-zip .
RUN unzip download-zip && mv ICE*/* /var/www/html/ && cd /var/www/html/ && chmod 757 lib/ data/ plugins/ tmp/
EXPOSE 80


