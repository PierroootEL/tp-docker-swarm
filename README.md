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
N'oubliez de modifier les chemins dans les Dockerfile présents dans les dossiers alertes et wordpress

## Lancez Wordpress et la base de données
```bash
cd tp-docker-swarm/wordpress
sh start_docker.sh
```
## Lancez le système d'alertes
```bash
cd  tp-docker-swarm/alerts/alertmanager/
sh start_docker.sh
```
## Lancez prometheus
```bash
cd  tp-docker-swarm/alerts/prom
sh start_docker.sh
```
## Lancez Node explorer
```bash
cd  tp-docker-swarm/alerts/node-exporter
sh start_docker.sh
```
