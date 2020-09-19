# Docker PostgreSQL 12.x and 13.x with pg_sphere

The following command will start a postgres 12 deamon with the pg_sphere module installed:

```bash
docker run --rm \
           --name pg-docker \
           -e POSTGRES_PASSWORD=<pass> \
           -d \
           -p 5432:5432 \
           -v <path to store data locally>:/var/lib/ \
           postgresql/data  
             douchy/pgsphere:{{TAG}}
```

The database can be accessed via:

```bash
docker exec -it pg-docker psql -U postgres -d postgres
```

Create the pg_sphere extension with:

```bash
docker exec -it pg-docker psql -c "CREATE EXTENSION pg_sphere;" -U postgres postgres
```

Test pg_sphere extension with:
```bash
psql -c "select spoint '(0.1,-0.2)';" -U postgres postgres
```

Expected output:
```sql
    spoint
--------------
 (0.1 , -0.2)
(1 row)
```

# Container

Visit [https://hub.docker.com/r/douchy/pgsphere](https://hub.docker.com/r/douchy/pgsphere)

Container available for posgres 12.x and 13.x on Debian and Alpine:
- Debian
 - postgres 12.x `docker pull douchy/pgsphere:12.0.1`
 - postgres 13.x `docker pull douchy/pgsphere:13.0.1`

# Acknowledgments

The docker image is provided by [ldouchy](https://hub.docker.com/r/douchy/pgsphere).

This fork uses the fix for PostgreSQL 12 by [mdgomes](https://github.com/mdgomes/pgsphere).

For more information, have a look at [https://pgsphere.github.io/](https://pgsphere.github.io/) and [https://github.com/akorotkov/pgsphere](https://github.com/akorotkov/pgsphere)

