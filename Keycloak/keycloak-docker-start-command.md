### Keycloak start

Command to start the Keycloak authorization server container.

Change port configuration as needed, here given command will run keycloak server on port 8081.

```
docker run
    -p 8081:8080
    -d
    -e KC_BOOTSTRAP_ADMIN_USERNAME=admin
    -e KC_BOOTSTRAP_ADMIN_PASSWORD=admin
    --rm
    --name key-clock-authorization-server
    quay.io/keycloak/keycloak:26.1.2
    start-dev
```

### docker-compose.yml file to run a Keycloak server with a MySQL database

Modify the environment variables, latest keycloak image and port as needed.

Here I'm running keycloak server on port 8081.

```
version: '3.8'

services:
  keycloak:
    image: quay.io/keycloak/keycloak:26.1.2
    container_name: key-clock-authorization-server
    environment:
      - KC_BOOTSTRAP_ADMIN_USERNAME=admin
      - KC_BOOTSTRAP_ADMIN_PASSWORD=admin
      - KC_DB=mysql
      - KC_DB_URL_HOST=host.docker.internal
      - KC_DB_URL_PORT=3306
      - KC_DB_URL_DATABASE=keycloak
      - KC_DB_USERNAME=root
      - KC_DB_PASSWORD=root
    ports:
      - '8081:8080'
    command: ['start-dev', '--import-realm']
    volumes:
      - ./realm.json:/opt/keycloak/data/import/realm.json
    restart: unless-stopped

```

```
volumes:
      - ./realm.json:/opt/keycloak/data/import/realm.json
```

This volumes configuration ensures persistent storage for realm configuration.

### Command to run the Compose file in detached mode.

`docker compose up -d`

### Command to stop docker compose

`docker compose down`
