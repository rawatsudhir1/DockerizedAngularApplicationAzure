FROM nginx:1.15.8-alpine AS nalpineimage
  RUN apk add --update nodejs nodejs-npm
  COPY . ./MY-APP/
  WORKDIR /MY-APP
  RUN npm install
  RUN $(npm bin)/ng build --prod

  FROM nginx:1.15.8-alpine
  COPY --from=nalpineimage /MY-APP/dist/my-app/ /usr/share/nginx/html