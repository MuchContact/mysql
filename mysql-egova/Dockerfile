FROM mysql:5.6
COPY data/ /docker-entrypoint-initdb.d
CMD ["--character-set-server=utf8mb4", "--collation-server=utf8mb4_unicode_ci"]