#on prend comme image de base ubuntu
FROM ubuntu:latest

#on fait les mise à jours et installe apache, php et mysql
RUN apt update && apt upgrade -y && DEBIAN_FRONTEND=noninteractive apt install -y apache2 php php-mysql nano

# Pour que le protocole TLS puisse fonctionner avec le Serveur HTTP Apache2, il faut activer le module ssl avec la commande :
RUN a2enmod ssl

# on copie nos fichier de configuration dans les dossier de apache
COPY wt12.ephec-ti.be.conf /etc/apache2/sites-available
COPY intra.wt12.ephec-ti.be.conf /etc/apache2/sites-available
COPY b2b.wt12.ephec-ti.be.conf /etc/apache2/sites-available

#création des liens symboliques
RUN ln -s /etc/apache2/sites-available/wt12.ephec-ti.be.conf /etc/apache2/sites-enabled
RUN ln -s /etc/apache2/sites-available/intra.wt12.ephec-ti.be.conf /etc/apache2/sites-enabled
RUN ln -s /etc/apache2/sites-available/b2b.wt12.ephec-ti.be.conf /etc/apache2/sites-enabled

# création du dossier cible pour les clés et certificats de tsl
RUN mkdir /etc/letsencrypt

# on copie les clés et certificats dans les dossier de letsencrypt
COPY wt12.ephec-ti.be.key /etc/letsencrypt/
COPY wt12.ephec-ti.be.crt /etc/letsencrypt/
COPY b2b.wt12.ephec-ti.be.key /etc/letsencrypt/
COPY b2b.wt12.ephec-ti.be.crt /etc/letsencrypt/
COPY intra.wt12.ephec-ti.be.key /etc/letsencrypt/
COPY intra.wt12.ephec-ti.be.crt /etc/letsencrypt/

# création du dossier cible pour les fichiers html
RUN mkdir /var/www/wt12.ephec-ti.be
RUN mkdir /var/www/b2b.wt12.ephec-ti.be
RUN mkdir /var/www/intra.wt12.ephec-ti.be

# on copie les fichier html
COPY wt12.ephec-ti.be.html /var/www/wt12.ephec-ti.be/index.html
COPY b2b.wt12.ephec-ti.be.html /var/www/b2b.wt12.ephec-ti.be/index.html
COPY intra.wt12.ephec-ti.be.html /var/www/intra.wt12.ephec-ti.be/index.html

#on expose le port 80 pour http et 443 pour https
EXPOSE 80 443
CMD apachectl -DFOREGROUND