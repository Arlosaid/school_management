# Utiliza una imagen oficial de Python como imagen padre
FROM python:3.11.7-slim-bullseye as prod

# Actualiza el sistema e instala dependencias necesarias
RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Instala virtualenv
RUN pip install --upgrade pip && pip install virtualenv

# Establece el directorio de trabajo en el contenedor
WORKDIR /app

# Crea un entorno virtual en el directorio /app/venv
RUN virtualenv venv

# Activa el entorno virtual
ENV PATH="/app/venv/bin:$PATH"

# Copia el archivo de dependencias
COPY requirements.txt /app/

# Instala las dependencias del proyecto
RUN pip install -r requirements.txt

# Copia el resto del código fuente del proyecto al contenedor
COPY . /app/

# Expone el puerto 8000
EXPOSE 3000

# Define el comando para ejecutar la aplicación
CMD ["python", "manage.py", "runserver", "0.0.0.0:3000"]

FROM prod as dev