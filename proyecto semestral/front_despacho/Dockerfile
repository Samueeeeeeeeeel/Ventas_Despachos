# Etapa 1: Construcción (Build)
FROM node:18-alpine as build
WORKDIR /app

# Copiamos los archivos de dependencias y las instalamos
COPY package*.json ./
RUN npm install

# Copiamos el resto del código y construimos la aplicación
COPY . .
RUN npm run build

# Etapa 2: Servidor (NGINX)
FROM nginx:alpine

# Copiamos el resultado de la construcción de React a la carpeta de NGINX
# Nota: Vite usa la carpeta 'dist'. Si usas Create React App, cambia 'dist' por 'build'
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]