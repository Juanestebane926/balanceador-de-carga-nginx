FROM node:lts-alpine

RUN mkdir /app
WORKDIR /app

# Copiar los archivos package.json y package-lock.json
COPY package*.json ./

# Instalar las dependencias
RUN npm install

# Copiar el resto del código de la aplicación
COPY . .

# Definir el comando para iniciar la aplicación en modo dev
CMD ["npm", "run", "dev"]