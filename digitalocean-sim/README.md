# Contenedor para simular un servidor
Para poder ejecutarlo utiliza este comando:

```shell
docker run -it --name digitalocean -p 2222:22 digitalocean-sim
```
```shell
docker run -d -p 5432:5432 -p 80:80 -p 22:22 --name digitalocean digitalocean
docker run -it --name digitalocean -p 3001:80 -p 5433:5432 digitalocean
```

- -it: Ejecuta el contenedor en modo interactivo.
- --name: Asigna un nombre al contenedor.
- -p 2222:22: Mapea el puerto 2222 de tu máquina al puerto 22 del contenedor (útil para SSH).

## Simular Servicios y Configuraciones
Dentro del contenedor, puedes:

- Instalar y configurar Nginx, Apache, Node.js, o cualquier stack que desees practicar.
- Configurar bases de datos como MySQL, PostgreSQL o MongoDB.
- Probar configuraciones de firewall (iptables, ufw).

## Guardar tu Progreso
Si realizas cambios en el contenedor y deseas guardarlos, puedes crear una nueva imagen basada en tu contenedor:


```shell
docker commit digitalocean digitalocean-sim:v2
```

## Simular SSH (Opcional)
Si instalaste un servidor SSH en el contenedor, puedes conectarte mediante:

Encuentra la dirección IP del contenedor:
```bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' digitalocean-container
```

Conéctate por SSH:
```bash
ssh developer@<IP_del_Contenedor> -p 2222
```


```bash
docker exec -it digitalocean bash
```

