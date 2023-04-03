# Ansible Collection - cadair.debops

This is a collection of roles (of varying quality) I have written which make use of the `debops.debops` collection to deploy various applications.

# Documentation

## Roles

### Babybuddy

This role deploys the [BabyBuddy](https://github.com/babybuddy/babybuddy) Django app using gunicorn.
A Python venv is created from which the app is deployed.

### Cloudlog

This role deploys the [cloudlog](https://github.com/magicbug/Cloudlog) php app.

#### Notes

The initial setup of the database must currently be done through the web UI.

### Photoprism

This role sets up [Photoprism](https://www.photoprism.app/), it downloads the source and compiles both the golang backend and js frontend on the target host.
It therefore uses the nodejs and golang debops roles to do so.

#### Notes

- The role forces the global nodejs version to 18.x and uses the nodejs upstream deb repos.
  You will probably need to put the following in your inventory for the host to make this work:
    ```
    nodejs__node_upstream: true
    nodejs__node_upstream_release: "node_18.x"
    nodejs__yarn_upstream: true
    ```
- A shell is configured for the photoprism user with the environment variables and PATH required to use the `photoprism` CLI tool.
- An hourly cron job is scheduled to reindex the library and a daily cron to convert files, if you want to disable these set `photoprism__default_cron_jobs: []`. You can configure extra cron jobs using `photoprism__cron_jobs: []`.


### Valheim

This role deploys a Valheim dedicated server based on the docker container from [llosche](https://github.com/lloesche/valheim-server-docker).
The role provisions the docker server and configures the container via environment variables.

## In Development Roles

### Mobilizion
