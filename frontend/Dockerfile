# Build stage
FROM node:20.18.1-alpine3.20 AS build
WORKDIR /app

# Actualizar paquetes del sistema
RUN apk update && apk upgrade --no-cache

COPY package*.json ./
RUN npm ci --ignore-scripts
COPY . .
RUN npm run build

# Production stage
FROM nginx:1.27-alpine

# Actualizar paquetes de nginx
RUN apk update && apk upgrade --no-cache

COPY --from=build /app/dist /usr/share/nginx/html

# Crear usuario no-root
RUN addgroup -g 1001 -S nginx-user && adduser -S nginx-user -u 1001
RUN chown -R nginx-user:nginx-user /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]