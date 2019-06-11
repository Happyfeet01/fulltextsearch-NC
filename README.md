# fulltextsearch-NC

With this Docker-Compose File you have an Setup for Fulltextsearch for Nextcloud.


#1. run this command at the root directory at your Server.

```
echo "vm.max_map_count=262144" >> /etc/sysctl.conf && sysctl -p
```
installing Docker-Compose
```
curl -L https://github.com/docker/compose/releases/download/$(curl -Ls https://www.servercow.de/docker-compose/latest.php)/docker-compose-$(uname -s)-$(uname -m) > /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose
```
Create and enter directory
```
mkdir -p /opt/docker-ncsearch && cd /opt/docker-ncsearch
```
Now you can create the docker-compose.yml

edit these Entrys:

```
- cluster.name=ncsearch
```
and the Volume for the persitant Data:

```
volumes:
  - /opt/docker-ncsearch/nc-data/:/usr/share/elasticsearch/data
```
