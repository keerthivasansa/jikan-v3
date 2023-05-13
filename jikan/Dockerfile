FROM php:8.1-apache-buster
ENV	COMPOSER_ALLOW_SUPERUSER	1
RUN	apt-get update && apt-get install -y \
	openssl \
	git \
	unzip \
	&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
	&& composer --version
RUN	git clone --branch=nightly-major --depth=1 https://github.com/pushrbx/jikan-rest . \
	&& composer require 'composer/package-versions-deprecated' \
	&& composer install --prefer-dist --no-progress --classmap-authoritative  --no-interaction \
	&& composer update jikan-me/jikan
ADD	.env	/run-jikan.sh	./
RUN chmod +x run-jikan.sh
ENTRYPOINT	["./run-jikan.sh"]
