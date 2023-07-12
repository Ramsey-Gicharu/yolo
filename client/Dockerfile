#specify a base image
FROM node:alpine

#specify the working directory
WORKDIR /app

#copying the required dependencies file
COPY package.json .

#installing dependencies
RUN npm install

#copying app source code
COPY . .

#specifying the container port
EXPOSE 3000

#command to start the application
 CMD ["npm", "start"]