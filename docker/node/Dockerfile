FROM node:16.14.0-alpine AS base

RUN mkdir /app

FROM base AS development

WORKDIR /app

FROM base AS production

RUN mkdir /build
COPY . /build

WORKDIR /build

RUN rm -rf /build/node_modules \
    && npm i \
    && npm run build \
    && mv /build/build /app/ \
    && rm -rf /build/*

COPY . /build

RUN rm -rf /build/node_modules \
    && npm i --only=prod \
    && mv /build/node_modules /app/ \
    && rm -rf /build

WORKDIR /app
