#  Build the React application
FROM node:18-alpine AS build
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application files and build
COPY . .
RUN npm run build

# Serve the application using Nginx
FROM nginx:alpine

# Copy the build output from the previous stage to Nginx's html folder
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80 for the browser
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
