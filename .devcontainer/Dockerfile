FROM ubuntu:focal
ENV TZ=America/Sao_Paulo
ARG DEBIAN_FRONTEND=noninteractive

# install basic packages
RUN apt update && apt full-upgrade -y && apt install -y \
    apt-transport-https \
    build-essential \
    curl \
    fzf \
    git \
    gnupg \
    gnupg2 \
    htop \
    locales \
    locales-all \
    php-cli \
    php-curl \
    php-xml \
    php-mysql \
    php-mbstring \
    php-gd \
    php-json \
    php-zip \
    software-properties-common \
    tmux \
    unzip \
    vim \
    wget \
    zsh \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/

# install nodejs
RUN curl -sL https://deb.nodesource.com/setup_14.x  | bash -
RUN apt-get -y install nodejs \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/

# install gulp globally
RUN npm install -g gulp yarn npm-check-updates prettier

# install oh my zsh
RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# install docker
RUN apt-get update \
    && apt-get install -y apt-transport-https ca-certificates curl gnupg2 lsb-release \
    && curl -fsSL https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/gpg | apt-key add - 2>/dev/null \
    && echo "deb [arch=amd64] https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list \
    && apt-get update \
    && apt-get install -y docker-ce-cli \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/

# install docker-compose
RUN LATEST_COMPOSE_VERSION=$(curl -sSL "https://api.github.com/repos/docker/compose/releases/latest" | grep -o -P '(?<="tag_name": ").+(?=")') \
    && curl -sSL "https://github.com/docker/compose/releases/download/${LATEST_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# install composer
COPY --from=composer:1.10.17 /usr/bin/composer /usr/local/bin/composer

# install github cli
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key C99B11DEB97541F0 \
    && apt-add-repository https://cli.github.com/packages \
    && apt update \
    && apt install -y gh \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/

# configure pt_BR locale
ENV LC_ALL pt_BR.UTF-8
ENV LANG pt_BR.UTF-8
ENV LANGUAGE pt_BR.UTF-8

# docker configuration
COPY ./scripts/docker-debian.sh /tmp/library-scripts/
RUN apt-get update && bash /tmp/library-scripts/docker-debian.sh \
  && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/
ENTRYPOINT ["/usr/local/share/docker-init.sh"]

# change shell to zsh
RUN chsh -s ~/.zshrc
CMD ["zsh"]
