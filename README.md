# fulltextsearch-NC

With this Docker-Compose File you have an Setup for Fulltextsearch for Nextcloud.


#1. run this command at the root directory at your Server.

    # $ echo "vm.max_map_count=262144" >> /etc/sysctl.conf && sysctl -p # execute on [host]
    # $ curl -L https://github.com/docker/compose/releases/download/$(curl -Ls https://www.servercow.de/docker-compose/latest.php)/docker-compose-$(uname -s)-$(uname -m) > /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose
    # $ mkdir -p /opt/docker-ncsearch && cd /opt/docker-ncsearch
    # $ # <Save this file as docker-compose.yml>
    # $ 
# $ 

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
create an Dockerfile to install the correct Version of Elasticsearch and Ingest-Attachment
```
mkdir -p elasticsearch && echo -e "FROM docker.elastic.co/elasticsearch/elasticsearch-oss:7.1.1\nRUN /usr/share/elasticsearch/bin/elasticsearch-plugin install --batch ingest-attachment" > docker-elasticsearch/Dockerfile
```

Set the correct permission:

```
mkdir -p /opt/docker-ncsearch/elasticsearch-data && chown 1000:1000 /opt/docker-ncsearch/elasticsearch-data/ -R
```
Now you can create the docker-compose.yml and edit these Entrys:

```
- cluster.name=ncsearch #needed at the FTS Backend at nextcloud
```
and the Volume for the persitant Data:

```
volumes:
  - /opt/docker-ncsearch/elasticsearch-data/:/usr/share/elasticsearch/data
```
