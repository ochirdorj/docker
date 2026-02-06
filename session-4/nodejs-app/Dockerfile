FROM node:20-alpine

WORKDIR /app

COPY package.json /app/package.json

RUN npm install

COPY app.js /app/app.js

EXPOSE 3000

USER node

CMD ["npm", "start"]