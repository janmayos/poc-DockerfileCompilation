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