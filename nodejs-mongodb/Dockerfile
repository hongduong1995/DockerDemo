FROM node:12-alpine

WORKDIR /app

COPY ["package.json","package-lock.json","./"]

RUN npm install

COPY  ./src .

CMD ["node","app.js"] 