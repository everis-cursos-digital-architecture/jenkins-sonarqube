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

> Acceder a Jenkins desde <http://ec2-18-202-252-187.eu-west-1.compute.amazonaws.com:8080/>

* Abrir el contenido del fichero de clave privada (everis-curso-jenkins.pem) para permitir la conexión por SSH entre ambas instancias.
    ```pem
    -----BEGIN RSA PRIVATE KEY-----
    (Replace with the initial of the teacher's name)IIEpQIBAAKCAQEApc7G3LpiwRdPslwlXLveQvrsX9pKUiZJbPVU+2iI4HUb+fyeCjexJAZjEgB7
    eOdf+yswyEiM1zxMf7BL416bqSYqrOVEG8SjJIxpEtC2jBni4BxsE4SWLss0U5C/u54bPR+9/ZqL
    6V52RSjoKctNdzRzhvcD5bXKd07tBGDLhKOMhMSCbfRxV2feNm1oVLKcJsfdaRiDdvZcrDH6lRXh
    vU6GBix9BOp1SE+roqR20h4JjmVKq/e2WvC+DzzJZlshBu0tU6QYWxhnfsF3zSUkKcqrES+0lu8C
    7H44R65gkBMl61YddUU9MNgisHP65r12zer+bFlOKPvicOsILWh+IwIDAQABAoIBAQCNG4LGCqFM
    rugWZLEvUHsBCcbsdDvX2dmXLtqZ8wa57zBV+ZUOIQNSI1Vg1qQ96rsWaFVlvciOzDRWXtTWtYdH
    1sFuzta9wwUMb6pkZtdUOBuKmuWnXqjpPepUS9XAd/e6dy8bitETVF7W0M9z8h8FGdBPxhy8+49J
    JhQ0K6RIRf41glCKDpLkS0qpWjiMO889PDkNl9BM9q5cz5GmMbga/ovGiKUYEIG+XP4iVd1crNaF
    g2kyNC40OiEXtHZnKCvydv43uER+E+kweQlB6orVhtGeJPMl01fvkVZ6K+lRVuUv5PMRTUCKkxuw
    O0UfYp/t8Oj4yfexyF+YClrtoiChAoGBAOmqBNkuQDFTEJYBDxGYSNYrBn4OQMZSHdV0pvkzu2JR
    fy0UZgGoVqLtQaIXmyrdz9bsxQTNkBSpF+OeA9rUwVoXH8/11eS1dZQaCCHXe8Jjgs1Jn5dvGOUd
    GrqKPIRg+dAgcUpJL0Wmx1M0bYKqq1Frn4RiOg2RWAIUKhonZeE7AoGBALWoP2PdjCXcA0W6GMFu
    kzt0MGI8+f1ThWhBZwusC0rKGlpYEKg/hAPJFPAzUoRaaaGKlbZ4o6Xg/ljeYfcwwAP4kunCt8rp
    cjZcOOtZWN7nzq1Z41U9w9JuAvSAsLxQlhZt4ea5aLJss2UCgahjsUhnF5HAq1qSl0QeUkL3Fog5
    AoGAFRmTQoFYrpuPndwOnkogGabc+TkURFRZ+VKFWW+Adkphr5Jt+6xV1nSSPq7fBintgLz0tZBS
    eGskixtTwckAhMAd0Uujuvlf2rXXEidBN7aAs0T4slYH63iLV1jwSgvvwwmK8WhWanW6/hp34RrE
    SZ/sUaoFEACV7+oeOypfms0CgYEAmn7/erXgDgrylYjSqSCcA8Krq8Fkc/lmyuZk915ZNEBy7Udc
    01tBsd6A+lEL6xjiIcu1zL0JoXibmYV5GDzT8gylFj7PBbpJssX4euFAXkQUWQbL+6FOPFfoF36j
    0WVQYL8Pk6U40Bb28/+PumEfVA6p0wJkOeHW2M5Y9C8lcLECgYEAs+LzJ5DM6cTYf+SMsEyWPMGW
    F3FufBoYteASD/l06EoN9Pk/jBOazLuZE3vYGu0y7WBj5yUvFfM3z7Ha0aifooViJ/mIEbUgcBaw
    j/25VQ2gpwP6+CMNaYtc1bCPKtVlU++8QULialrv7tU1IduOuR1KYUeY7n0nUQISTOgeTG0=
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