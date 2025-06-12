FROM node:20-alpine

LABEL author="ar4kiara" maintainer="ar4kiara@gmail.com"

RUN apk add --no-cache \
    git \
    curl \
    build-base \
    python3 \
    py3-pip \
    chromium \
    chromium-chromedriver \
    cairo-dev \
    pango-dev \
    jpeg-dev \
    giflib-dev \
    librsvg-dev \
    && adduser -D -h /home/container container

# Install PM2 globally as root
RUN npm install -g pm2@latest --unsafe-perm

# Copy entrypoint.sh and give execute permissions as root
COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

# Install Python packages
RUN pip3 install --upgrade pip setuptools wheel

CMD [ "/bin/sh", "/entrypoint.sh" ] 