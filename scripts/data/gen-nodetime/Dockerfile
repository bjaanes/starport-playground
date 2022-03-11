FROM node:alpine

RUN apk add --no-cache \
    build-base \
    git \
    libplist-dev \
    libplist-static \
    openssl-dev \
    openssl-libs-static

WORKDIR /root

RUN git clone git://git.saurik.com/ldid.git

WORKDIR /root/ldid

RUN g++ -pipe -o ldid ldid.cpp -I. -x c lookup2.c -lcrypto -lplist-2.0 -Os -fwhole-program -flto -s -static

WORKDIR /root/nodetime

COPY src src
COPY nodetime nodetime
COPY package.json package.json
COPY package-lock.json package-lock.json
COPY tsconfig.json tsconfig.json

RUN npm i

ENV PATH="/root/ldid:${PATH}"

RUN npm run build