FROM postgres:14.1-alpine

ENV POSTGRES_DB=db \
	POSTGRES_USER=usr \
	POSTGRES_PASSWORD=pwd

COPY ./scripts/ /docker-entrypoint-initdb.d 
