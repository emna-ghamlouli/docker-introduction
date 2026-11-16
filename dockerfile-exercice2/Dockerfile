
# ==================================================
# ANCIEN TRAVAIL (conservé en commentaire)
# ==================================================

# Utiliser une image de base Node.js légère
# FROM node:18-alpine

# Définir le répertoire de travail
# WORKDIR /app

# Copier les fichiers package.json et package-lock.json
# COPY package.json package-lock.json ./

# Copier les fichiers sources
# COPY . .

# Installer les dépendances
# RUN npm install

# Installer le serveur
# RUN npm install -g serve

# Construire l'application
# RUN npm run build


# EXPOSE 3000
# CMD ["serve", "-s", "dist", "-p", "3000"]


# ==================================================
# NOUVEAU TRAVAIL : BUILD MULTI-ÉTAPES SÉCURISÉ
# ==================================================

# Première étape : construction
# Stage 1: Build the application
FROM node:22.23.5-alpine3.24 AS builder
 
WORKDIR /app
 
COPY package.json package-lock.json ./
 
RUN npm ci
 
COPY . .
 
RUN npm run build
 
# Stage 2: Run the application
FROM nginxinc/nginx-unprivileged:1.31.7-alpine3.24 AS production
 
COPY --from=builder --chown=101:101 /app/dist/ /usr/share/nginx/html/
 
USER 101
 
EXPOSE 8080
 