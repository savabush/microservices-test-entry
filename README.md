# Microservices Test

Test task for using microservices with [FastAPI](https://fastapi.tiangolo.com/), [uvicorn](https://www.uvicorn.org/), [Tortoise ORM](https://tortoise-orm.readthedocs.io/en/latest/), [asyncpg](https://www.asyncpg.org/), [Redis](https://redis.io/) and [AIOKafka](https://pypi.org/project/aiokafka/).

## Links for repositories of services

1. [bet-maker](https://github.com/savabush/microservices-test-bet-maker)
2. [line-provider](https://github.com/savabush/microservices-test-line-provider)

## Install and deploy

1. We are using docker compose here, so first of all, you need to install docker and docker compose. 
2. Then we need to clone our repositories and copy `.env.example` file to `.env`.
3. Make changes for environment variables in `.env` file.
4. Build services with `docker build -t <image_name> -f docker/Dockerfile .`
5. And after that run `docker-compose up -d`.
   1. If there are errors, just check logs.
6. Now we need to initialize our db. So run `docker compose exec <SERVICE_NAME> aerich init-db`
7. In every repo we have folder `migrations`. `Aerich` does not provide creating schemas, so we need to create them manually in psql `docker compose exec <POSTGRES_HOST> psql -U <POSTGRES_USER> <POSTGRES_DB>`.
8. Copy `SQL` code from migraions and paste it to console. Everything should be fine.
9. Now we need to upgrade migratoins to heads `docker compose exec <SERVICE_NAME> aerich upgrade`

## Features

More of features that was added are overhead. They are not needed by task, but why not.

1. Health checkers in docker compose and on API's.
2. Replicas for each microservice.
3. Transactional Outbox pattern and SAGA for event sourcing. 
4. Added migrations.
5. Kafka is used for keep atomicity and consistency.
6. `Outbox` table is created for checking events and log changes of them.

## Tests

We are using pytest and coverage here.

1. To run tests you can use this command. But remember, you need to install all dependencies before that.
```bash
pytest
```

2. To check coverage you can use this command.
```bash
coverage run -m pytest
```

3. To get report of coverage you can use this command.

```bash
coverage report -m
```
