#  Building the React application
FROM node:18-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
# Build with relative base path to avoid path issues in Nginx
RUN npx vite build --base=./

#  Serving files with Nginx
FROM nginx:alpine

# Clean Nginx default directory to prevent leftover files
RUN rm -rf /usr/share/nginx/html/*

# Copy the exact build output to Nginx server directory
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
