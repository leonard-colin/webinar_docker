FROM python:3.9

# Configuration courante de Python pour Docker
ENV PYHTONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

# Définition du répertoire de travail
WORKDIR /app

# Instalation des dépendances générales avec apt
RUN apt update && apt install --no-install-recommends -y \
    # Dépendances pour compiler des paquets Python
    build-essentiel \
    # Dépendance pour construire psycopg2
    libpq-dev
    # Eliminer ce qui est inutile

# Installation des dépendances Python
COPY ./requirements.txt .
# optimisation : RUN pip install --no-cache-dir --no-index -r requirements.txt
RUN pip install --no-cache-dir --no-index -r requirements.txt

COPY ./compose/local/django/entrypoint /entrypoint
# Substituer les \r à la fin d'une ligne si scrypt sur Windows
RUN sed -i 's/\r$//g' /entrypoint
RUN chmod +x /entrypoint

COPY ./compose/local/django/start /start
# Substituer les \r à la fin d'une ligne si scrypt sur Windows
RUN sed -i 's/\r$//g' /start
RUN chmod +x /start

# Spécification de la commande démarrage
ENTRYPOINT [ "/entrypoint" ]