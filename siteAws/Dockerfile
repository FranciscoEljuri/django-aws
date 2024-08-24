# Usar la imagen oficial de Python como base
FROM python:3.10-slim

# Instalar dependencias del sistema necesarias para mysqlclient
RUN apt-get update && apt-get install -y \
    gcc \
    default-libmysqlclient-dev \
    pkg-config \
    build-essential \
    --no-install-recommends && rm -rf /var/lib/apt/lists/*

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar el archivo de requisitos y luego instalarlos
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

# Instalar el cliente MySQL
RUN apt-get update && apt-get install -y default-mysql-client

# Copiar todo el contenido de la aplicación al contenedor
COPY . /app/

# Exponer el puerto 8000 para que esté disponible fuera del contenedor
EXPOSE 8000

# Comando para ejecutar la aplicación Django
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
