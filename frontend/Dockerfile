# # # Use an official Node.js runtime as a parent image
# # FROM node:16 as build

# # # Set the working directory in the container
# # WORKDIR /app

# # # Copy package.json and package-lock.json to the working directory
# # COPY package*.json ./

# # # Clear npm cache
# # RUN npm cache clean --force

# # # Remove both package-lock.json and node_modules (if they exist)
# # RUN rm -rf package-lock.json node_modules

# # # Install dependencies with a retry mechanism
# # RUN npm install --retry=5 --no-optional

# # # Install Rollup explicitly
# # RUN npm install -D rollup

# # # Copy the rest of the application to the working directory
# # COPY . .

# # # Build the application
# # RUN npm run build

# # # Use a smaller nginx image to serve the build
# # FROM nginx:alpine

# # # Copy the build output from the previous stage
# # COPY --from=build /app/build /usr/share/nginx/html

# # # Expose port 80
# # EXPOSE 80

# # # Start nginx server
# # CMD ["nginx", "-g", "daemon off;"]


# # Stage 1: Build the frontend
# FROM node:16 as build

# WORKDIR /app

# COPY package*.json ./

# RUN npm install --quiet

# COPY . .

# RUN npm run build

# # Stage 2: Serve the frontend with Nginx
# FROM nginx:alpine

# COPY --from=build /app/build /usr/share/nginx/html

# EXPOSE 80

# CMD ["nginx", "-g", "daemon off;"]


# Stage 1: Build React App
FROM node:16 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install --retry=5 --no-optional
COPY . .
RUN npm run build

# Stage 2: Serve React App with Nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
