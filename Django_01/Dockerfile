# Usar la imagen oficial de Ubuntu como base
FROM ubuntu:22.04

# Evitar preguntas interactivas durante la instalación
ENV DEBIAN_FRONTEND=noninteractive

# Actualizar el sistema e instalar Python y pip
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv python3-dev build-essential && \
    apt-get clean

# (Opcional) Instalar git y otras herramientas útiles
RUN apt-get install -y git curl nano

# Establecer Python3 como comando por defecto para 'python'
RUN ln -s /usr/bin/python3 /usr/bin/python

# Carpeta de trabajo dentro del contenedor
WORKDIR /mysite/mysite

COPY . /mysite

COPY requirements.txt /mysite/mysite
RUN pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]