# Use an official Node.js runtime as the base image
FROM node:12-alpine

# Set the working directory inside the container
WORKDIR /app/backend

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install the dependencies
RUN npm install

# Install Express and MongoDB driver
RUN npm install express mongodb --save

# Copy the remaining app files to the container
COPY . .

# Set the environment variable for the frontend URL
ENV REACT_APP_FRONTEND_URL=http://localhost:3000

# Expose the container's port
EXPOSE 5000

# Start the Node.js server
CMD ["npm", "start"]

