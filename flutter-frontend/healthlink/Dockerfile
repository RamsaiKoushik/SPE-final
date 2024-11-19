# Step 1: Build Flutter Web App
FROM dart:stable AS build

WORKDIR /app

# Copy Flutter project files
COPY . .

# Get dependencies
RUN dart pub get

# Build the web app
RUN flutter build web

# Step 2: Serve the Flutter Web App with Nginx
FROM nginx:alpine

# Copy built Flutter web app to Nginx directory
COPY --from=build /app/build/web /usr/share/nginx/html

# Expose port 80 for Nginx
EXPOSE 80
