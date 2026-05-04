# Utilise Node.js 20 sur Alpine Linux pour plus de légèreté
FROM node:20-alpine

# Définit le dossier de travail
WORKDIR /app

# Copie les fichiers de dépendances
COPY package*.json ./

# Installe les dépendances
RUN npm install

# Copie le reste des fichiers du projet (src, app.js, etc.)
COPY . .

# Expose le port 3001
EXPOSE 3001

# Commande pour démarrer l'API
CMD ["node", "src/app.js"]