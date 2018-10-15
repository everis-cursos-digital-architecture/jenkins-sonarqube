# Curso Jenkins y Sonarqube Básico y Avanzado

## Instalación Jenkins en instancias EC2 de AWS

```bash
# Ejecutamos la actualización de repositorios de Linux e instalación de unzip.
sudo yum update -y
sudo yum install -y unzip
sudo yum install -y git

# Instalación de Java y seteo del Path para el sistema.
sudo yum remove java-1.7.0-openjdk -y
sudo yum install java-1.8.0-openjdk-devel -y

# Descarga e instalación de Jenkins
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
sudo yum clean all
sudo yum install jenkins -y
sudo service jenkins start
```

> Documentación instalación en diferentes plataformas: <https://jenkins.io/doc/book/installing/>

## Configuración de esclavos Jenkins en instancias EC2 de AWS

> Acceder a Jenkins desde <ec2-52-51-107-81.eu-west-1.compute.amazonaws.com:8080/>

* Abrir el contenido del fichero de clave privada (everis-curso-jenkins.pem) para permitir la conexión por SSH entre ambas instancias.
    ```pem
    -----BEGIN RSA PRIVATE KEY-----
    Enviar a los alumnos
    -----END RSA PRIVATE KEY-----
    ```
* Jenkins > Administrar Jenkins > Administrar nodos > Nuevo nodo.
* Establece un nombre descriptivo al esclavo y selecciona `Permanent Agent`.
* Configuración:
  * **Directorio raíz:** `/home/ec2-user`
  * **Metodo de ejecución:** `Arrancar agentes remotos en máquinas Unix vía SSH`
  * **Nombre de máquina:** `Dirección IP asociada a cada alumno`
  * **Credentials :** `Add > SSH Username (ec2-user) with private key (Primer punto)`
  * **Host Key Verification Strategy:** `Non verifying Verification Strategy`