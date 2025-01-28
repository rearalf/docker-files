FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# Instalar dependencias necesarias
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    vim \
    git \
    net-tools \
    sudo \
    ssh \
    build-essential \
    libssl-dev \
    postgresql \
    postgresql-contrib \
    && apt-get clean

# Crear usuario 'developer' y agregarlo al grupo sudo
RUN useradd -ms /bin/bash developer && echo "developer:password" | chpasswd && adduser developer sudo

# Establecer el directorio de trabajo
WORKDIR /home/developer

# Copiar el archivo .env al contenedor
COPY .env /home/developer/.env

# Usar envsubst para cargar las variables de entorno del archivo .env
RUN export $(cat /home/developer/.env | xargs) && \
    # Instalar Node.js 20.15.1 directamente sin NVM
    curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs && \
    # Verificar que Node.js se haya instalado correctamente
    node -v && \
    # Configurar PostgreSQL
    /etc/init.d/postgresql start && \
    sudo -u postgres psql -c "CREATE USER $POSTGRES_USER WITH PASSWORD '$POSTGRES_PASSWORD';" && \
    sudo -u postgres psql -c "CREATE DATABASE $POSTGRES_DB OWNER $POSTGRES_USER;" && \
    sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE $POSTGRES_DB TO $POSTGRES_USER;"

# Exponer puertos
EXPOSE 22 3000 80 5432

# Establecer el comando por defecto
CMD [ "/bin/bash" ]
