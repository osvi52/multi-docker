FROM node:18-alpine as builder

###WORKDIR '/app'
WORKDIR /usr/app

###COPY ./package.json ./
COPY --chown=node:node ./package.json ./

RUN npm install -g npm@8.16.0 

###RUN mkdir node_modules/.cache && chmod -R 777 node_modules/.cache

###COPY . .
###COPY . ./
COPY --chown=node:node . ./

USER node

RUN npm run build
##

FROM nginx
EXPOSE 3000

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /usr/app/build /usr/share/nginx/html