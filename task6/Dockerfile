FROM node:12-alpine

COPY package.json .
COPY package-lock.json .

RUN npm install

COPY . .

RUN npm build

