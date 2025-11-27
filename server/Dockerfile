# server/Dockerfile
FROM node:18-alpine

# create and use app directory
WORKDIR /usr/src/app

# copy only package files first (better cache)
COPY package*.json ./

# install dependencies
RUN npm install

# copy rest of the code
COPY . .

# if your backend runs on 5000, change if needed
EXPOSE 5000

# start command (change if you use something else)
CMD ["npm", "start"]
