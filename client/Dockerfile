# Use a Node.js base image with Node.js 12 and Alpine
FROM node:12-alpine AS build

# Set the working directory in the container
WORKDIR /app/client

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
