# Configuración de Docker con Nginx y Flask
Este repositorio describe los pasos necesarios para configurar un contenedor Docker con Nginx y Python instalado. También configura Nginx como proxy inverso para enrutar las solicitudes del endpoint `/pagina` hacia una aplicación Flask que se ejecuta en el puerto 5000.


## Requisitos previos
- Tener instalado Docker y Docker Compose en tu sistema.
- Conexión a internet para descargar las imágenes necesarias.

## Descarga de imagenes en docker
```bash
docker pull nginx
```
 Ponemos el nombre nginx y lo mapeamos al en el puerto 80:80 y especificamos la version de nginx a utilizar en este caso la ultima 
```bash
docker run -d --name nginx -p 80:80 nginx:latest
```
## Pasos

1. Verificar las imagenes que tienes
```bash
docker ps
```
2. Inicializamos el contenedor de nginx (si esta detenido)
   ```bash
   docker start nombredelcontenedor
   ```
3.  Verificamos que el contenedor este encendido y con el puerto correspondiente
     ```bash
     docker ps -a
     ``
4.   Abrimos una terminal dentro del contenedor para que puedas escribir comandos directamente dentro de él.
 ```bash
docker exec -it 53900ea88a8f bash
```
5. Creamos un usuario.
    ```bash
    adduser aileen
    ```
Actualizamos 
con
```bash
 apt update
```
y hacemos el  que nos pide
```bash
apt list --upgradable
```

Instalamos python 
```bash
 apt install -y python3.11 
 ```
Instalemos un editor ya sea nano o vim
```bash
apt install -y vim
```
Instalemos flask
```bash
pip install Flask
```
Creamos el archivo de flask en nuestro usuario siguiendo los pasos de la pagina 
```bash
https://flask.palletsprojects.com/en/3.0.x/
```

Una ves estando  activado el . .venv/bin/activate
creamos nuestro archivo  vim hello.py
editando esta parte a  " @app.route("/pagina")" para evitar que nginx se confunda.

Ingresamos en la carpeta /etc/nginx/conf.d
y editamos
```bash
vim default.conf
```
![Archivo default](/default.png)

Resultado:
![Archivo default](/resultado.png)


