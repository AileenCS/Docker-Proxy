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
4.   Abrimos una terminal dentro del contenedor para que puedas escribir comandos directamente dentro de él(indicar el ID del contenedor o bien, el nombre que le asignamos)
 ```bash
docker exec -it 53900ea88a8f bash
```
5. Creamos un usuario.
    ```bash
    adduser aileen
    ```
    al dar enter nos pedira poner una contraseña
  ```bash   New password:
Retype new password:
passwd: password updated successfully
Changing the user information for user
Enter the new value, or press ENTER for the default
        Full Name []: user
        Room Number []: 1234
        Work Phone []: 1234
        Home Phone []: 1234
        Other []: 1234
Is the information correct? [Y/n] y
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
En el root:
Instalamos python 
```bash
 apt install -y python3.11
 ```
En el root:
Instalamos el .venv de pyton

```bash
Apt Install -y python3.11-venv. 
 ```
En el mismo root

Instalemos un editor ya sea nano o vim
```bash
apt install -y vim
```
en el root:
Instalemos flask
```bash
pip install Flask
```
Ingresamos a nuestro usuario 
```bash
su aileen 
```
Creamos el archivo de flask en nuestro usuario siguiendo los pasos de la pagina https://flask.palletsprojects.com/en/3.0.x/installation/
```bash
 mkdir myproject
$ cd myproject
```
crear el entorno virtual con 
python3 -m venv .venv
verificar  que se activo correctamente el entorno:
```bash
. .venv/bin/activate
```

creamos nuestro archivo  vim hello.py
```bash
 vim hello.py
```
```bash
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
```
editando esta parte a  " @app.route("/pagina")" para evitar que nginx se confunda.
guardamos con el comando :wq
exit para salir de donde estamos pero ingresamos a nuestro usuario 
su aileen 

Ingresamos en la carpeta 
```bash
cd /etc/nginx/conf.d 
```
Si listamos los archivos (ls) aparece un archivo de nombre default.conf.
y este lo editamos  para redirigir las solicitudes a la aplicación Flask  
```bash
vim default.conf
```
![Archivo default](/default.png)

No borramos nada solo le agregamos
```bash
location /pagina{ proxy_pass http://127.0.0.1:5000; }
```
location /pagina: Esto le dice a Nginx que cualquier persona que visite http://tu_dominio.com/pagina debe ser manejada de una manera especial.
proxy_pass http://127.0.0.1:5000;: Aquí le estás diciendo a Nginx que, cuando alguien entre a http://tu_dominio.com/pagina, redirija esa solicitud a un servidor que está corriendo en tu computadora (localhost), en el puerto 5000. Este servidor podría ser tu aplicación Flask, por ejemplo.


Reiniciar nginx por completo
```bash
nginx -s reload
```


Regesanos a ejecutar a nuestro archivo
```bash
su aileen
pwd
cd
cd myproject
python3 -m venv .venv
. .venv/bin/activate

flask --app hello run
```
Resultado:
Acceda http://localhost/pagina

![Archivo default](/resultadoo.png)


