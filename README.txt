Base docs
https://www.digitalocean.com/community/tutorials/how-to-install-drupal-with-docker-compose


-Build- stil WIP due to permission issues
cp env.default .env
make the necessary changes to .env

cd
mkdir -p data/drupal/sites
docker run --rm drupal:9.2.10 tar -cC /var/www/html/sites . | tar -xC ./data/drupal/sites
docker-compose up -d
docker-compose exec drupal mkdir -p /var/www/html/sites/default/files
docker-compose exec drupal cp /var/www/html/sites/default/default.settings.php /var/www/html/sites/default/settings.php
docker-compose exec drupal chmod 660 /var/www/html/sites/default/settings.php
docker-compose exec drupal chown www-data:www-data /var/www/html/sites/default/settings.php
docker-compose exec drupal chown www-data:www-data /var/www/html/sites/default/files
http://localhost:8080/
docker-compose exec drupal chmod 440 /var/www/html/sites/default/settings.php

-Destroy-
docker-compose down
docker-compose rm
docker volume rm 
docker volume rm drupal-voting-views_db-data
docker volume rm drupal-voting-views_drupal-data
docker volume rm drupal-voting-views_drupal-modules
docker volume rm drupal-voting-views_drupal-profiles
docker volume rm drupal-voting-views_drupal-sites
docker volume rm drupal-voting-views_drupal-themes

-Notes-
-- If init-ing into a volume
docker-compose run --rm -v drupal-sites:/temporary/sites drupal:9.2.10 cp -aRT /var/www/html/sites /temporary/sites
