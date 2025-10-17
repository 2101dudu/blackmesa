# Install

Immich version v2.0.0 

1. Get docker-compose file:
    ```bash
    wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
    ```


2. Get .env file:
    ```bash
    wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env
    ```

3. Start container:
    ```bash
    docker compose up -d
    ```


# Backup

# Restore backup

```bash
docker compose down -v # CAUTION! Deletes all Immich data to start from scratch

# CAUTION! Deletes all Immich data to start from scratch
# uncomment next line to completly purge all data
# rm -rf ./postgres

docker compose create
docker start immich_postgres
sleep 10

gunzip --stdout "/home/debian/immich-db-backup-1754100000009.sql.gz" \
| sed "s/SELECT pg_catalog.set_config('search_path', '', false);/SELECT pg_catalog.set_config('search_path', 'public, pg_catalog', true);/g" \
| docker exec -i immich_postgres psql --dbname=postgres --username=postgres  # Restore Backup

# uncomment next line to bypass postregs' user password (otherwise, the .env file has to mactch the backup's postgres' user password
# docker exec -i immich_postgres psql --username=postgres --dbname=postgres -c "ALTER USER postgres PASSWORD 'postgres';"

docker compose up -d
```

TODO:
add restart unless stopped to compose file


