# Start Master:
```
docker run -d -P \
  -v "${PWD}"/replication-entrypoint.sh:/usr/local/bin/replication-entrypoint.sh \
  --name mysql_master \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=1 \
  -e MYSQL_SERVER_ID=1 \
  bergerx/mysql-replication:5.7
```
# Start Master 2
  1. 启动备份库
      ```
      docker run -d -P \
        -v "${PWD}"/replication-entrypoint.sh:/usr/local/bin/replication-entrypoint.sh \
        --name mysql_master_back \
        -e MYSQL_ALLOW_EMPTY_PASSWORD=1 \
        -e MYSQL_SERVER_ID=2 \
        bergerx/mysql-replication:5.7
      ```
  1. 配置主从
      ```
      CHANGE MASTER TO
        MASTER_HOST='master-ip',
        MASTER_USER='root',
        MASTER_PASSWORD='',
        MASTER_PORT=master-port,
        MASTER_LOG_FILE='log-file',
        MASTER_LOG_POS=log-pos,
        MASTER_CONNECT_RETRY=10;
      ```

# Start Slave(同步Master2)
```
docker run -d -P \
  -v "${PWD}"/replication-entrypoint.sh:/usr/local/bin/replication-entrypoint.sh \
  --name mysql_slave \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=1 \
  -e MYSQL_SERVER_ID=3 \
  --link mysql_master_back:master \
  bergerx/mysql-replication:5.7
```
