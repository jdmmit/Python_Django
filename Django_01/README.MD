# 🚀 Docker Ubuntu + Python + Django

¡Bienvenido! Este proyecto te ayuda a crear un contenedor Docker con Ubuntu, Python y Django, ideal para desarrollo, pruebas o aprendizaje.  

> ![Docker + Python](https://raw.githubusercontent.com/docker-library/docs/master/python/logo.png) <!-- Imagen sugerida, puedes cambiar el link -->

---

## 📝 Requisitos previos

- Tener instalado **Docker** en tu computador.

---

## 📦 ¿Qué incluye esta imagen?

- 🐧 Ubuntu 22.04
- 🐍 Python 3 (con pip, venv y herramientas de desarrollo)
- 🛠️ Git, curl y nano (puedes agregar más si quieres)
- 🎉 Django (instalado a través de `requirements.txt`)

---

## ⚡ Instrucciones rápidas

### 1️⃣ Clona este repositorio o crea una carpeta nueva

```bash
git clone <URL-de-tu-repo>
# o simplemente crea una carpeta y entra en ella
mkdir mi-proyecto-docker
cd mi-proyecto-docker
```

---

### 2️⃣ Crea el archivo Dockerfile

Copia este contenido en un archivo llamado `Dockerfile` (sin extensión):

```Dockerfile
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv python3-dev build-essential && \
    apt-get clean

RUN apt-get install -y git curl nano

RUN ln -s /usr/bin/python3 /usr/bin/python

WORKDIR /app

COPY . /app

COPY requirements.txt /app/
RUN pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

---

### 3️⃣ (Opcional) Agrega tus archivos de Python y Django

- Puedes copiar tus scripts `.py`, archivos de Django o un archivo `requirements.txt` a la carpeta `/app` para que se incluyan en la imagen.
- Si tienes un `requirements.txt`, agrega esto al Dockerfile **antes del CMD**:

```Dockerfile
COPY requirements.txt /app/
RUN pip install -r requirements.txt
```

---

### 4️⃣ Construye la imagen de Docker

```bash
docker build -t django_01 .
```

---

### 5️⃣ Corre el contenedor y sincroniza tu carpeta

```bash
docker run -it -v ${PWD}:/app -p 8000:8000 django_01
```

- **`-v $(pwd):/app`** sincroniza tu carpeta local con la del contenedor.
- **`-p 8000:8000`** expone el puerto del servidor Django.

---

### 6️⃣ Accede a tu servidor Django

Abre tu navegador y entra a:  
[http://localhost:8000](http://localhost:8000)

---

## 💡 Notas

- El servidor Django se mantendrá corriendo hasta que decidas apagar el contenedor.
- Todos los cambios en tu carpeta local se reflejan automáticamente en el contenedor.
- Puedes modificar el Dockerfile para instalar más cosas según lo que necesites.
- Si tienes dudas o errores, revisa los mensajes que te da Docker, suelen ser bastante claros.

---

