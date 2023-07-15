# Use an official Node.js runtime as the base image
FROM node:14-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the working directory
COPY package*.json ./

# Install app dependencies
RUN npm install

# Copy the entire app directory to the working directory
COPY . .

# Set environment variables, if required
# ENV REACT_APP_API_URL=https://api.example.com

# Expose the desired port (default is 3000 for a React app)
EXPOSE 3000

# Start the React app (use the "start" script defined in package.json)
CMD ["npm", "start"]
