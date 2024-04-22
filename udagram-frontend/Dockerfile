### Build
FROM node:16 AS builder

## Create app directory
WORKDIR /usr/src/app

## Install app dependencies
## A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./
RUN npm ci

## Bundle app source
COPY . .

## Install Ionic globally
RUN npm install -g @ionic/cli

## Build Ionic app
RUN ionic build

### Run
FROM nginx:alpine

## Copy built app from previous stage
COPY --from=builder /usr/src/app/www /usr/share/nginx/html
