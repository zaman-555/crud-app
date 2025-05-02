# Stage 1: Build the React app
FROM node:18-alpine as build

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

COPY . ./

RUN npm run build

# Stage 2: Serve the built app with Nginx
FROM nginx:alpine

# Copy Nginx config
COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf

# Copy built assets from build stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]