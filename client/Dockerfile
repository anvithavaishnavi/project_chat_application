# build stage
FROM node:18-alpine as build

WORKDIR /app

# set legacy openssl flag for webpack/react-scripts
ENV NODE_OPTIONS=--openssl-legacy-provider

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# run stage
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
