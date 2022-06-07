# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.195.0/containers/php/.devcontainer/base.Dockerfile
# [Choice] PHP version (use -bullseye variants on local arm64/Apple Silicon): 8, 8.0, 7, 7.4, 7.3, 8-bullseye, 8.0-bullseye, 7-bullseye, 7.4-bullseye, 7.3-bullseye, 8-buster, 8.0-buster, 7-buster, 7.4-buster, 7.3-buster

ARG VARIANT=8
FROM mcr.microsoft.com/vscode/devcontainers/php:0-${VARIANT}

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ENV APACHE_RUN_USER=$USERNAME

# Install Composer from: https://hub.docker.com/_/composer
COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN  echo 'export PATH="$PATH:$HOME/.composer/vendor/bin:/root/.composer/vendor/bin:vendor/bin"' >> /root/.bashrc

ENV DEBIAN_FRONTEND=noninteractive
ENV SS_ENVIRONMENT_TYPE="dev"
ENV SS_DATABASE_CLASS="MySQLDatabase"
ENV SS_DATABASE_SERVER="db"
ENV SS_DATABASE_USERNAME="root"
ENV SS_DATABASE_PASSWORD="secret"
ENV SS_DATABASE_NAME="silverstripe"
ENV SS_DEFAULT_ADMIN_USERNAME="admin"
ENV SS_DEFAULT_ADMIN_PASSWORD="admin"

RUN echo 'SetEnv SS_ENVIRONMENT_TYPE dev' >> /etc/apache2/conf-enabled/environment.conf
RUN echo 'SetEnv SS_DATABASE_CLASS MySQLDatabase' >> /etc/apache2/conf-enabled/environment.conf
RUN echo 'SetEnv SS_DATABASE_SERVER db' >> /etc/apache2/conf-enabled/environment.conf
RUN echo 'SetEnv SS_DATABASE_USERNAME root' >> /etc/apache2/conf-enabled/environment.conf
RUN echo 'SetEnv SS_DATABASE_PASSWORD secret' >> /etc/apache2/conf-enabled/environment.conf
RUN echo 'SetEnv SS_DATABASE_NAME silverstripe' >> /etc/apache2/conf-enabled/environment.conf
RUN echo 'SetEnv SS_DEFAULT_ADMIN_USERNAME admin' >> /etc/apache2/conf-enabled/environment.conf
RUN echo 'SetEnv SS_DEFAULT_ADMIN_PASSWORD admin' >> /etc/apache2/conf-enabled/environment.conf

# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && apt-get -y install --no-install-recommends mariadb-client libzip-dev libicu-dev \
   && docker-php-ext-configure zip  \
   && docker-php-ext-install zip \
   && docker-php-ext-install bcmath \
   && docker-php-ext-install mysqli \
   && docker-php-ext-configure intl \
   && docker-php-ext-install intl

RUN echo "alias sake='vendor/bin/sake'" >> /home/$USERNAME/.bashrc
