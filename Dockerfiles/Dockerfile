# Base
FROM node:12-alpine as base

WORKDIR /app

COPY *.json ./

RUN npm ci && npm cache clean --force

COPY ./src ./src

RUN npm run prebuild
RUN npm run build

# Application
FROM node:12-alpine as app

WORKDIR /app
COPY package*.json ./
RUN npm ci --production && npm cache clean --force
COPY --from=base /app/dist ./dist

USER node
ENV PORT=8080
EXPOSE 8080

CMD [ "npm", "run", "start:prod" ]
