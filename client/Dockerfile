# Use an official Node.js runtime as the base image
FROM node:14-alpine

# Set the working directory inside the container
WORKDIR /app/frontend
# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the remaining app files to the container
COPY . .

# Set the environment variable for the backend URL
ENV REACT_APP_BACKEND_URL=http://localhost:5000/api/products
ENV REACT_APP_MONGODB_URL=mongodb://mongo:27017/yolomy

# Expose the container's port
EXPOSE 3000

# Build the React app
RUN npm run build

CMD ["npm", "start"]