FROM node:18.8-alpine@sha256:8437bc872a71f3b15a384ff32d098a68e06b440c0d9ec3eb4b4fa26ca16f2b30 as base

FROM base as builder

WORKDIR /home/node/app
COPY package*.json ./

COPY . .
RUN yarn install
RUN yarn build

FROM base as runtime

ENV NODE_ENV=production

WORKDIR /home/node/app
COPY package*.json  ./
COPY yarn.lock ./

RUN yarn install --production

EXPOSE 3000

CMD ["node", "dist/server.js"]
