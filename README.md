# poc-DockerfileCompilation
Configuración de infra de compilación con Jenkins y agentes con Alpine
Maven 8 agente

Generar Imagen
* docker build -t maven-8ssh:latest -f .\DockerFileMavenAlpine .

Generar Contenedor
* docker run -d -p 20228:22 --name mvn-jdk8 maven-8ssh:latest

Entrar al contenedor por SSH
* ssh root@localhost -p 20228
  * Contraseña: root

Verificar si el ssh esta activo
    docker exec -it mvn-jdk8 /bin/sh
Verifica los procesos en ejecución
    * ps aux
Inicia el servicio sshd
    * /usr/sbin/sshd

Docker agente

 Pasos para usar Docker dentro del contenedor en Windows
Habilita el acceso al socket de Docker
Abre Docker Desktop y ve a:

Settings → General → Activa "Expose daemon on tcp://localhost:2375 without TLS"
Guarda y reinicia Docker Desktop.

* Construir la imagen Docker:
    * docker build -t docker-java17-ssh:latest -f .\DockerFile-DockerSSH .
* Ejecutar el contenedor
    * Con privilegios
        * docker run -d --privileged -p 20229:22 --name jenkins-agent docker-java17-ssh:latest
    * Normal
        * docker run -d -p 20229:22 --name jenkins-agent docker-java17-ssh:latest
* Acceder desde exec
    * Con privilegios
        *  docker exec --privileged -it jenkins-agent /bin/sh
    * Normal
        *  docker exec  -it jenkins-agent /bin/sh
* Acceder al contenedor por SSH
 *  ssh root@localhost -p 20229