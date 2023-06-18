## Script to sync gids and uids between host and container

### Steps to use this script:

1. In docker compose define users and groups you want to sync, and copy host configuration in read only mode.

```
volumes:
    - /etc/passwd:/etc/passwd.src:ro
    - /etc/group:/etc/group.src:ro
environment:
    - host_users=www-data,mysql
    - host_groups=www-data,mysql,staff
```

2. Copy script `docker-sync-ids.sh` to your container.

Example:
```
COPY deploy/docker-sync-ids.sh /tmp/docker-sync-ids.sh
RUN chmod a+x /tmp/docker-sync-ids.sh
```

3. Run this script before services are launched.

```
# env setup

/tmp/docker-sync-ids.sh

# launch services
```
