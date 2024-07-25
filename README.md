# Lancer un site WordPress avec Docker

Ce guide vous explique comment configurer et lancer un site WordPress à l'aide de Docker. Tous les fichiers nécessaires sont disponibles dans ce dépôt Git.

## Prérequis

Assurez-vous d'avoir les outils suivants installés sur votre machine :
- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Git](https://git-scm.com/)

## Cloner le dépôt

Commencez par cloner ce dépôt sur votre machine locale :

```bash
git clone https://github.com/PierroootEL/tp-docker-swarm.git
cd tp-docker-swarm
```
## Préparation de l'infrastructure
Copier le fichier " node_exporter " présent dans le  dossier " files ", dans le répertoire " /usr "
Créez un service dans " /etc/systemd/system/ " nommé " node-exporter.service "
```bash
cd /etc/systemd/system/
nano node-exporter.service
```
Ajouter :
```
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=nobody
Group=nogroup
Type=simple
ExecStart=/usr/node_exporter
Restart=always

[Install]
WantedBy=multi-user.target
```
IMPORTANT : N'oubliez de modifier les chemins dans les fichiers docker-compose.yml présents dans les dossiers " alerts " et " wordpress " afin de changer les chemins absolu à destination des volumes
## Partie WEB :
### Lancez Wordpress et la base de données
```bash
cd tp-docker-swarm/wordpress
sh start_docker.sh
```
## Partie MONITORING :
### Lancez Node explorer
```bash
systemctl start node-exporter.service
systemctl enable node-exporter.service
```
### Lancez le système d'alertes
```bash
cd  tp-docker-swarm/alerts/alertmanager/
sh start_docker.sh
```
### Lancez prometheus
```bash
cd  tp-docker-swarm/alerts/prom
sh start_docker.sh
```
