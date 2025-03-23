# l'image de base Python 3.8 Buster
FROM python:3.8-buster

# Informations du mainteneur
LABEL maintainer="EquipeMP <ayoub.jarhni@gmail.com>"

# Copier le fichiers student_age.py 
COPY student_age.py /

# Installation des prérequis
RUN apt update -y && apt install python3-dev libsasl2-dev libldap2-dev libssl-dev -y

# Copier le fichiers requirements.txt
COPY requirements.txt /

# Installer les dépendances Python
RUN pip3 install -r /requirements.txt

# Créer le dossier de données 
RUN mkdir -p /data

# déclarer le dossier comme volume
VOLUME ["/data"]

#Port 
EXPOSE 5000
# Commande de démarrage
CMD ["python3", "/student_age.py"]
