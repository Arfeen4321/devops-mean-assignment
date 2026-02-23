# ==============================
# Stage 1 - Build Angular App
# ==============================
FROM node:18 AS build

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Build Angular app (production by default in Angular 15)
RUN npm run build


# ==============================
# Stage 2 - Serve with Nginx
# ==============================
FROM nginx:alpine

# Remove default nginx config
RUN rm -rf /etc/nginx/conf.d/default.conf

# Copy Angular build output
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

# Copy custom nginx config for SPA fallback
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
