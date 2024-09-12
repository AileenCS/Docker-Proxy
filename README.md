# Configuración de Docker con Nginx y Flask
Este repositorio describe los pasos necesarios para configurar un contenedor Docker con Nginx y Python instalado. También configura Nginx como proxy inverso para enrutar las solicitudes del endpoint `/pagina` hacia una aplicación Flask que se ejecuta en el puerto 5000.

## Requisitos previos

- Tener instalado Docker y Docker Compose en tu sistema.
- Conexión a internet para descargar las imágenes necesarias.


##Descarga de imagenes en docker
```bash
docker pull nginx


