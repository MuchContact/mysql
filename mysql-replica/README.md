```
docker run -d -P \
  -v "${PWD}"/replication-entrypoint.sh:/usr/local/bin/replication-entrypoint.sh \
  --name mysql_master \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=1 \
  -e MYSQL_SERVER_ID=1 \
  bergerx/mysql-replication:5.7
```