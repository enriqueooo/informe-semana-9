# Práctica: Contenerización de Aplicación React y Backend con Docker

## 1. Título  
**Contenerización de aplicación React y backend con Docker para visualización de datos mediante API REST**

## 2. Tiempo de duración  
**90 minutos**

## 3. Fundamentos  

Esta práctica tiene como objetivo construir y contenerizar una aplicación frontend desarrollada con React que muestra una tabla con datos obtenidos desde una API REST alojada en un contenedor backend. Se aprenderá a construir imágenes Docker personalizadas para ambos proyectos y a orquestar su ejecución conjunta mediante `docker-compose`, garantizando la comunicación entre contenedores en la misma red Docker.

## 4. Conocimientos previos

- Fundamentos de Docker y docker-compose.
- Conocimientos básicos de React.
- Entendimiento básico de APIs REST.
- Manejo de terminal y comandos Docker.

## 5. Objetivos a alcanzar

- Crear un proyecto backend con Node.js que exponga una API REST con datos de una entidad específica.
- Crear un proyecto frontend con React que consuma la API y muestre los datos en una tabla.
- Contenerizar ambos proyectos mediante Docker.
- Orquestar ambos contenedores para que se comuniquen correctamente utilizando docker-compose.

## 6. Equipo necesario

- Docker y docker-compose instalados.
- Node.js y npm instalados.
- Editor de código (VS Code, etc).
- Navegador web.

## 7. Material de apoyo

- [Docker Docs](https://docs.docker.com/)
- [React Docs](https://reactjs.org/docs/getting-started.html)
- [Node.js Docs](https://nodejs.org/en/docs/)

---

## 8. Procedimiento

### Paso 1: Crear proyecto backend

- Inicializar proyecto Node.js.
- Implementar API REST que entregue datos JSON de la entidad.
- Definir puerto de escucha (ej. 5000).

### Paso 2: Crear Dockerfile para backend

En la carpeta del backend, crear archivo `Dockerfile`:

```Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 5000
CMD ["npm", "start"]
```
## Paso 3: Crear proyecto frontend con React

- Inicializar un proyecto React, por ejemplo, usando `create-react-app`:

  ```bash
  npx create-react-app nombre-del-proyecto
  
  ```
  ## Paso 4: Crear Dockerfile para frontend

En la carpeta del frontend, crea un archivo llamado `Dockerfile` con el siguiente contenido:

```Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
EXPOSE 3000
```
## Paso 5: Crear archivo `docker-compose.yml`

Este archivo orquesta ambos servicios y permite la comunicación entre ellos:

```yaml
version: '3.8'

services:
  backend:
    build:
      context: ./backend
    ports:
      - "5000:5000"

  frontend:
    build:
      context: ./frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend
```
## 9. Resultados esperados

- Ambas imágenes Docker deben construirse sin errores.
- El backend debe exponer la API en el puerto 5000.
- El frontend debe correr en el puerto 3000 y mostrar la tabla con datos del backend.
- La comunicación entre contenedores debe ser funcional y transparente.

---

## 10. Bibliografía

- [Docker Docs](https://docs.docker.com/)
- [React Official Docs](https://reactjs.org/)
- [Node.js Docs](https://nodejs.org/)
## 11. Audio
https://drive.google.com/file/d/1QzVRQqNuw4O00jsfBeXqzr8cwFVuwQfy/view?usp=sharing
