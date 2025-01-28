# Contenedor para simular un servidor
Para poder ejecutarlo utiliza este comando:

```bash
docker build -t nombre_imagen .
```
Construye una imagen Docker desde el archivo `Dockerfile` en el directorio actual (`.`). Asigna un nombre a la imagen usando `-t nombre_imagen`.

Con `docker run` empiezas a crear el contenedor segun la imagen que agregues.

```bash
docker run nombre_imagen --name nombre_contenedor -p puerto_host1:puerto_contenedor1 -p puerto_host2:puerto_contenedor2 -p puerto_host3:puerto_contenedor3
```

- `-it`:
    - `i`: Mantiene la entrada estándar (stdin) abierta, lo que permite interactuar con el contenedor.
    - `-t`: Asigna una pseudo-terminal para una experiencia de línea de comandos interactiva.
- `-name`: Agrega el nombre del contenedor.
- `-p`: Agregar los puertos que quieres usar, `host:contenedor` para decir cuales vas a abrir y a cuales se van a enlazar.

```shell
docker run nombre_imagen -it --name nombre_contenedor -p puerto_host1:puerto_contenedor1
```

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

## Entrar al bash del contenedor
Para esto debes de encender el contenedor.

```bash
docker start nombre_contenedor
```

Luego ejecutas el contendor en modo interactivo con `-it` y al final el bash para ejecutar la consola. 
```bash
docker exec -it nombre_contenedor bash
```

- `docker exec`: Este subcomando de Docker se utiliza para ejecutar un comando dentro de un contenedor que ya está en ejecución.
- `-it`:
    - `i`: Mantiene la entrada estándar (stdin) abierta, lo que permite interactuar con el contenedor.
    - `-t`: Asigna una pseudo-terminal para una experiencia de línea de comandos interactiva.
- `bash`: Es el comando que deseas ejecutar dentro del contenedor. En este caso, abre un intérprete de comandos (shell) basado en bash dentro del contenedor.