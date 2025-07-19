# Repo to deploy Airflow, Dozzle and Postgres as simple containers.

Repo created with the goal of documenting how an Airflow "prod" environment works, since most of the Airflow tutorials teach how to deploy locally. These services were deployed in a Cloud VPS, and the DAGs are automatically imported from a DAGs repo, using Github Actions.
Next step: Implement Kubernetes.

## Requirements:
- In standby mode with all services running, it consumes 4 GB RAM. So, at least 6 GB of RAM and 4 vCPUs.

## Steps:
- [Install Docker Engine](https://docs.docker.com/engine/install/);
- Clone this repo;
- Create .env files in Airflow and Postgres folders;
- Run Docker Compose up for Dozzle -> Postgres -> Airflow.
- Airflow is accessible at ip:8080, Dozzle at ip:8888.

## [Airflow 3.0.3](https://github.com/apache/airflow): 
- Tasks orchestration.

### Airflow .env:
```sh
AIRFLOW_UID = 
_AIRFLOW_WWW_USER_USERNAME = 
_AIRFLOW_WWW_USER_PASSWORD = 
DB_HOST = 
DB_PORT = 
DB_USER = 
DB_PASS = 
DB_NAME = 
```

## [Postgres 16.9](https://www.postgresql.org/):
- It deploys two Postgres containers: one for data and another for the Airflow Metadata Database.

### Postgres .env:
```sh
PG_DATA_USER = 
PG_DATA_PASS = 
PG_DATA_DB = 
PG_AIRFLOW_USER = 
PG_AIRFLOW_PASS = 
PG_AIRFLOW_DB = 
```

## [Dozzle](https://github.com/amir20/dozzle):
- Container logging, RAM, and CPU observability.

### Dozzle user authentication generation: 

By default, the users.yml file contains the credentials for the user admin/password, but if you'd like different credentials, navigate to dozzle/data and run the command below to generate a new users.yml file:

```sh
docker run -it --rm amir20/dozzle generate admin --password password --email test@email.net --name "John Doe" > users.yml
```
