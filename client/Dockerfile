#Defining the image we wnat to build from
FROM node:alpine 

#Specifying the work directory
WORKDIR /app

#Copying the required dependencies file
COPY package.json package.json

#Installing Dependencies 
RUN npm install

#Copying App source code
COPY .  .

#Specifying the Container Port
EXPOSE 3000

#Command to start the application
CMD ["npm", "start"]
