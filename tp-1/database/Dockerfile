FROM postgres:14.1-alpine

ENV POSTGRES_DB=db \
   POSTGRES_USER=usr \
   POSTGRES_PASSWORD=pwd

# From "Init database" part
COPY setup-db /docker-entrypoint-initdb.d/