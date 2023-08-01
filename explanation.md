# Client side Image creation Justification
For the client side docker image I used a Node:alpine image to reduce the overall image size 
# dockefile directives used for client side dockerfile
# Defining the image we wnat to build from
# Choice of the base image on which to build each container.
so for both the backend and front end I choose to use a node:12-alpne imagine beacuse the node version needed for the application was node 12 and I chooe alpine as the image falvour due to its small size and less vulnerabilities \
# Dockerfile directives used in the creation and running of each container.

Frontend dockerfile data with reasons for each directive

# Use a Node.js base image with Node.js 12 and Alpine
FROM node:12-alpine AS build

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the source code into the container
COPY . .

# Set the environment variable for the backend URL
ENV REACT_APP_API_URL=http://localhost:5000/api/products
ENV REACT_APP_MONGODB_URL=mongodb://mongo:27017/yolomy


# Build the React app
RUN npm run build

# Create the production-ready container using Nginx
FROM nginx:alpine

# Copy the built React app to the Nginx web server directory
COPY --from=build /app/build /usr/share/nginx/html

# Copy the custom Nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose the port to the outside world
EXPOSE 80

# Start Nginx when the container is launched
CMD ["nginx", "-g", "daemon off;"]


backend docker file directives with reasons as comments 

# Use an official Node.js runtime as the base image
FROM node:12-alpine

# Set the working directory inside the container
WORKDIR /app/backend

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the remaining app files to the container
COPY . .

# Set the environment variable for the frontend URL
ENV REACT_APP_FRONTEND_URL=http://localhost:3000

# Expose the container's port
EXPOSE 5000

# Start the Node.js server
CMD ["npm", "start"]

# Docker-compose Networking (Application port allocation and a bridge network implementation) where necessary.
I set up one network for communication between the frontend, backend and MongoDb known as yolo-project-network the reason for this is I did not see a need for mulltiple networks to connect the containers when only one network is very much capable of the same.

The ports choosen for the backend ports are 5000:5000 reaosn beaing the sevrve locally runs on port 5000 and i wanted to maintain the same port for docker

The ports choosen for the frontend are 3000:80 being that the local port is 3000 and the reason for choosing port 80 on the docker port is cause I set up a nginx sever running at port 80 I found to be the best  solution towards the 404 error when building a docker compose image.
# Docker-compose volume definition and usage (where necessary).
so for the volumes in each and every service I defined a volume within Mongodb, frontend, backend this is to ensure that data is persistence is maintained even locally and have the containers quickly start with already cached data in the volumes

# Git workflow used to achieve the task.
I forked the given repository shared in the task requirements and cloned it within my pc and then consistently did git commits with the chnages made in my local repo and pushed the changes to the master branch in git hub .

# DockerHub Backend Image link
https://hub.docker.com/r/rgicharu/backend-project-image

# Dockerhub Frontend Image link
https://hub.docker.com/r/rgicharu/frontend-project-image

# Vagrant Virtual Machine provisioning with Ansible to run dockerized MERN APP 

# step One
I did a vagrant init with the generic 22.04 ubuntu base image 
# step two
1) I worked on the play book first updating the cache.
2) Fetching the docker repository
3) Updated the cache 
4) Downloaded docker and docker compose on virtual machine
5) Added vagrant user to the docker group to allow the virtual machine user to run docker commands without sudo
6) Enabled and started the docker services
7) I installed dependencies needed for docker in vagrant i.e python
8) I then cloned my project repository and set up a directory for it on the virtual machine 
9) Performing tests I already had data volumes in my repository and I realised from research this made my mongo container crush thus from research I found a solution to creating an ansible playbook task  that could enable automatic deletion of the data volume at vagrant up --provison command
10) I also wrote down a task to install npm and node as well as moongose in the vagrant virtual machine while running npm install within the backend folder in the virtual machie to ensure my backend was properly configured with all dependencies.
11) I wrote ddown a task to run the containers automatically once the virtual machine is up and provisioned allowing the end user to access the web application form the host machine  by simply typing localhost:3000 on their browser and esnuring data persistence through correct cinfiguration of the containers running from docker compose.
# step 3
Created a hosts file and a ansible.cfg file to allow for more hosts and greater host management if the need ever arises as it is best practices to have this.


