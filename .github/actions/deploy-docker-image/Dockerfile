# ARG pour définir le chemin vers le dossier target
ARG TARGET_DIR=target

# ARG pour la configuration JVM
ARG XMX=512m
ARG XMS=256m

# ARG pour les profils Spring
ARG SPRING_PROFILES=docker

# ARG pour le port
ARG PORT=8080

# Utiliser l'image de base Eclipse Temurin JRE 21 Alpine (plus légère)
FROM eclipse-temurin:21-jre-alpine

# Créer un utilisateur non-root pour la sécurité
RUN addgroup -g 1001 -S appgroup && \
    adduser -S appuser -u 1001 -G appgroup

# Définir le répertoire de travail
WORKDIR /app

# Copier le JAR depuis le chemin spécifié
COPY ${TARGET_DIR}/*.jar app.jar

# Changer le propriétaire du fichier
RUN chown appuser:appgroup app.jar

# Basculer vers l'utilisateur non-root
USER appuser

# Exposer le port configuré
EXPOSE ${PORT}

# Variables d'environnement
ENV SPRING_PROFILES_ACTIVE=${SPRING_PROFILES}
ENV JAVA_OPTS="-Xmx${XMX} -Xms${XMS}"
ENV SERVER_PORT=${PORT}

# Point d'entrée de l'application
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]