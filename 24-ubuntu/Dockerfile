FROM ubuntu:22.04

LABEL author="ar4kiara" maintainer="ar4kiara@gmail.com"

RUN apt update && apt install -y \
    git \
    ca-certificates \
    curl \
    build-essential \
    libtool \
    python3 \
    python3-pip \
    chromium-browser \
    chromium-chromedriver \
    pkg-config \
    libcairo2-dev \
    libpango1.0-dev \
    libjpeg-dev \
    libgif-dev \
    librsvg2-dev

# Install Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_24.x | bash - && \
    apt install -y nodejs

# Install PM2 globally as root
RUN npm install -g pm2@latest --unsafe-perm

# Add user
RUN useradd -m -d /home/container container

# Copy entrypoint.sh and give execute permissions as root
COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

# Install Python packages
RUN pip3 install --upgrade pip setuptools wheel

CMD [ "/bin/bash", "/entrypoint.sh" ] 
