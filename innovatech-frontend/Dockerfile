# --- ETAPA 1: Construcción ---
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# --- ETAPA 2: Servidor minimalista de producción ---
FROM nginx:1.25-alpine
# Copia la aplicación compilada al directorio público de Nginx
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]