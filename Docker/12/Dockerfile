FROM postgres:12 AS build

RUN apt-get update \
&& apt-get install -y --no-install-recommends \
	ca-certificates \
	make \
	git \
	gcc \
	postgresql-server-dev-12 \
&& cd /root \
&& git clone --depth 1 https://github.com/mdgomes/pgsphere.git \
&& cd pgsphere \
&& make USE_PGXS=1 PG_CONFIG=/usr/bin/pg_config \
&& make USE_PGXS=1 PG_CONFIG=/usr/bin/pg_config install 


FROM postgres:12

ENV POSTGRES_VERSION 12

COPY --from=build /usr/lib/postgresql/${POSTGRES_VERSION}/lib/bitcode/pg_sphere /usr/lib/postgresql/${POSTGRES_VERSION}/lib/bitcode/pg_sphere
COPY --from=build /usr/share/postgresql/${POSTGRES_VERSION}/extension/pg_sphere.control /usr/share/postgresql/${POSTGRES_VERSION}/extension/pg_sphere.control
COPY --from=build /usr/lib/postgresql/${POSTGRES_VERSION}/lib/pg_sphere.so /usr/lib/postgresql/${POSTGRES_VERSION}/lib/pg_sphere.so
COPY --from=build /usr/share/postgresql/${POSTGRES_VERSION}/extension/ /usr/share/postgresql/${POSTGRES_VERSION}/extension/

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]
