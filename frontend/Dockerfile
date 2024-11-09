# Step 1: Build React App

FROM node:alpine3.18 as build

# Setting up the work directory
WORKDIR /app

# Installing dependencies
COPY ./package.json ./
RUN npm install --legacy-peer-deps

# Copying all the files in our project
COPY . .

#src file - .env.aws
#dest file - .env
#copy all contents from .env.aws -> .env
RUN mv .env.aws .env

# Building our application
RUN npm run build

# Step 2: Server With Nginx - Inside docker containers itself nginx will have no need to install nginx separately on machine
FROM nginx:1.23-alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf *
COPY --from=build /app/build .

# Copy custom Nginx configuration file
COPY default.conf /etc/nginx/conf.d/default.conf


EXPOSE 80
ENTRYPOINT [ "nginx", "-g", "daemon off;" ]