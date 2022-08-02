# elasticsearch-workshop

### Connexion à votre instance linux
- Utiliser l'invite de commande directement si vous êtes sur Windows10
<img src=https://user-images.githubusercontent.com/73080397/182381175-0a91c49a-c047-4d97-9470-6b3f424d2e67.png width="500">
- Ouvrir le terminal si vous êtes sur MacOS
  ![open-folder-application-terminal](https://user-images.githubusercontent.com/73080397/182381582-8eb3bccb-c9bd-4c4d-acf5-f0e510b748a3.png)
- Sinon s'il le faut, installer [mobaXterm](https://download.mobatek.net/2022020030522248/MobaXterm_Portable_v20.2.zip) si vous êtes sur Windows
- Vos Credentials et IP respectives vous seront envoyés sur le chat
- Une clé SSH .pem vous sera transmise sur le chat
- si vous passez par MobaXterm ou Putty, vous devez convertir la clé du format .pem au format .ppk 
  voir ce mini [tuto](https://stackoverflow.com/questions/3190667/convert-pem-to-ppk-file-format)). 
  (**attention**, cette operation est souvent très hasardeuse au vu des différentes versions compatibles). 

- username : `ec2-user`
- adresse ip : `adresse ip fournie`
- options de connection : clé ssh ppk
- Se rendre dans le repertoire où vous  avez mis votre fichier pem
  Par exemple, si vous êtes sur windows et que vous l'avez mis dans le dossier téléchargements :
```
cd downloads
```
- et puis connectez-vous à l'instance EC2 :
 ```
ssh -i "cle-ssh.pem" ec2-user@ec2-addresse_ip.compute-1.amazonaws.com
```
![ter](https://user-images.githubusercontent.com/73080397/182382478-19512c71-e9e7-4367-8ed8-8d48ea4063f4.png)



Pour vérifier votre version de Linux (Centos ou Debian):
 ```
cat /etc/os-release
```
	
### Production Tools

- Installer les outils suivants : 
	- [VS Code](https://code.visualstudio.com/download)
	- [GitHub Desktop](https://help.github.com/en/desktop/getting-started-with-github-desktop/installing-github-desktop)
	- [ElasticSearch - The Definitive Guide ](https://drive.google.com/open?id=1dtJhgRiVfaTrqpDqi4MA4HRK5K2iWSr6)
- IMPORTANT : L'ouvrage vous est fourni à titre de démo, merci de penser aux auteurs et de l'acheter légalement

### Installation de Java 

- Si vous êtes sous AMZN Linux 2 (ce qui est très probablement le cas)

Il faut installer java 11 amazon corretto jdk :

```
sudo yum install java-11-amazon-corretto-headless
```

La version 17 installée par défaut sans spécifier la version n'est PAS encore compatible avec ES

- Si vous êtes sur Centos/RHEL

:warning: pensez à bien vérifier la compatibilité de la version de Java avec la version d'ES
(demander au formateur)

```
sudo yum install -y java
```


### Installation de wget 

```
sudo yum install -y wget
```

### Installation ElasticSearch

- Centos/RHEL/AMZN
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.6.2-x86_64.rpm
sudo rpm -i elasticsearch-7.6.2-x86_64.rpm
```
- Debian
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.6.2-amd64.deb 
sudo dpkg -i elasticsearch-7.6.2-amd64.deb
```

### Démarrage Service ElasticSearch
```
sudo service elasticsearch start
```

### Installation Logstash
- Centos/RHEL/AMZN
```
wget https://artifacts.elastic.co/downloads/logstash/logstash-7.6.2.rpm
sudo rpm -i logstash-7.6.2.rpm
```
- Debian
```
wget https://artifacts.elastic.co/downloads/logstash/logstash-7.6.2.deb
sudo dpkg -i logstash-7.6.2.deb
```

### Installation Kibana
- Centos/RHEL/AMZN
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.6.2-x86_64.rpm
sudo rpm -i kibana-7.6.2-x86_64.rpm
```
- Debian
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.6.2-amd64.deb
sudo dpkg -i kibana-7.6.2-amd64.deb
```

#### Configuration accès distant (remplacer localhost / 127.0.0.1 par 0.0.0.0) 

- Editer le fichier de conf
```
sudo vi /etc/kibana/kibana.yml
``` 
```
# Kibana is served by a back end server. This setting specifies the port to use.

server.port: 5601 <<<<<< ⚠⚠⚠ DECOMMENTER ÇA ⚠⚠⚠

# Specifies the address to which the Kibana server will bind. IP addresses and host names are both valid values.
# The default is 'localhost', which usually means remote machines will not be able to connect.
# To allow connections from remote users, set this parameter to a non-loopback address.

server.host: 0.0.0.0 <<<<<< ⚠⚠⚠ CHANGER ÇA ⚠⚠⚠
```

- Sauvegarder

### Démarrage Service Kibana
```
sudo service kibana start
```
### Vérifier le démarrage d'un service
```
sudo service nom_service status
```

### Vérification de votre accès Web

```
curl http://checkip.amazonaws.com
```
Sur votre navigateur, se rendre sur l'addresse suivante :
- http://votre.adresse.IP:5601
- Le logo charge et vous vous retrouvez tout de suite sur la page d'accueil de Kibana!

![kibana_home](https://user-images.githubusercontent.com/73080397/182124922-6cbcfe1c-bee4-455d-8190-f84c8a693737.png)
