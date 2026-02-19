# Usar versión específica y actualizada de Alpine para reducir vulnerabilidades
FROM node:20.18.1-alpine3.20

WORKDIR /app

# Actualizar paquetes del sistema para parchar vulnerabilidades
RUN apk update && apk upgrade --no-cache

COPY package*.json ./
RUN npm ci --omit=dev --ignore-scripts

COPY . .

# Crear usuario no-root para seguridad
RUN addgroup -g 1001 -S nodejs && adduser -S nodejs -u 1001
RUN chown -R nodejs:nodejs /app
USER nodejs

EXPOSE 3001
CMD ["node", "src/server.js"]