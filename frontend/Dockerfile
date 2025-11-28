# Stage 1: Build Angular app
FROM node:18 AS build

WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Copy the rest of the app and build production files
COPY . .
RUN ng build --configuration=production

# Stage 2: Serve app with Nginx
FROM nginx:alpine

# Copy built Angular app to Nginx html folder
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

# Copy custom Nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
