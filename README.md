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

2. inicializa el contenedor de nginx (si esta detenido)
   ```bash
   docker start nombredelcontenedor```
3.  verificamos que el docker este encendido y con el puerto correspondiente
     ```bash
     docker ps -a ```
4.   Ponemos el  comando
    ```bash
docker exec -it 53900ea88a8f bash
```
