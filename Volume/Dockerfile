FROM php:8-apache

WORKDIR /var/www/html/

COPY . .

EXPOSE 80

#Comando para o apache dar permissões ao docker
RUN chown -R www-data:www-data /var/www