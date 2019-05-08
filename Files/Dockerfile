FROM node:11.6.0-alpine AS nalpineimage
COPY . ./MY-APP
WORKDIR /MY-APP
RUN npm i
RUN $(npm bin)/ng build --prod

FROM nginx:1.15.8-alpine
COPY --from=nalpineimage /MY-APP/dist/my-app/ /usr/share/nginx/html