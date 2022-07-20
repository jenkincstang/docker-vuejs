# build stage
FROM node:lts-alpine as build-stage
WORKDIR /app
COPY ./package*.json ./
RUN npm install
COPY ./ .
RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# docker build -t docker-vuejs:nginx -f ./nginx/Dockerfile .
# docker run --name docker-vuejs-nginx-demo -it -p 8082:80 -d  docker-vuejs:nginx
