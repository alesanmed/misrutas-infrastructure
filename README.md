# Mis Rutas Infrastructure
This repo contains the files needed to bring the pre-requisites for the Mis Rutas repos up.

## NATS
For runnig [NATS](https://nats.io/) you just have to execute:

```shell
cd nats
docker-compose up -d
```

That will run NATS using the config defined in `nats/config/nats.conf`. The queue will be listning for clients on port 4222.

The credentials for connecting to the queue are defined in the config file:

```conf
authorization {
  user: root
  password: password
}
```

## PostgreSQL
Running [PostgreSQL](https://www.postgresql.org/) is exactly the same, just execute:

```shell
cd postgres
docker-compose up -d
```

That will run a postgres database server on port 5432 and the [pgAdmin](https://www.pgadmin.org/) panel on port 80.

The credentials for connecting to the database server are defined in the compose file:

```
environment:
  POSTGRES_USER: user
  POSTGRES_PASSWORD: password
```

Also, the pgAdmin section is in the same dockerfile:

```dockerfile
pgAdmin:
  image: dpage/pgadmin4
  restart: always
  environment:
    PGADMIN_DEFAULT_EMAIL: root@email.com
    PGADMIN_DEFAULT_PASSWORD: password
  ports:
    - 80:80 
  networks:
    - db
```

The credentials to access the admin panel are also there and if you don't want the panel at all you just have to comment the whole block.
