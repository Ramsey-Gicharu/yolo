# Use an official Node.js runtime as the base image
FROM node:14-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the project dependencies
RUN npm install

# Copy the application code to the working directory
COPY . .

# Build the React app for production
RUN npm run build

# Expose the desired port (e.g., 3000)
EXPOSE 3000

# Set environment variables
ENV REACT_APP_BACKEND_URL=http://localhost:5000/api/products

# Start the React app
CMD ["npm", "start"]
