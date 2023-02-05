# Hasura & Monk

This repository contains Monk.io template to deploy Hasura & Monk either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

## Prerequisites

- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

### Make sure monkd is running

```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository

```bash
git clone https://github.com/monk-io/hasura
```

## Load Template

```bash
cd hasura
monk load MANIFEST
```

### Let's take a look at the themes I have installed

```bash
foo@bar:~$ monk list hasura
✔ Got the list
Type      Template               Repository  Version  Tags
runnable  hasura/hasura     local       -        -
runnable  hasura/hasura-db  local       -        -
group     hasura/stack      local       -        -
```

## Deploy Stack

```bash
foo@bar:~$ monk run hasura/stack
? Select tag to run [local/hasura/stack] on: monk
✔ Starting the job: local/hasura/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% hasura/graphql-engine:latest monk
✔ [================================================] 100% postgres:latest monk
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ local/hasura/stack has been already running

🔩 templates/local/hasura/stack
 └─🧊 Peer monk
    ├─🔩 templates/local/hasura/hasura
    │  └─📦 67d75658c522844d9dd7dc06dfcb35bb-hasura-hasura-hasura
    │     ├─🧩 hasura/graphql-engine:latest
    │     ├─💾 /var/lib/monkd/volumes/growthbook -> /usr/local/src/app/packages/back-end/uploads
    │     └─🔌 open <ip>:8080 (0.0.0.0:8080) -> 8080
    └─🔩 templates/local/hasura/hasura-db
       └─📦 a629918e0a1b6bd1632846fd0476e99a-hasura-hasura-db-postgres
          ├─🧩 postgres:latest
          └─🔌 open <db_ip>:5432 (0.0.0.0:5432) -> 5432

💡 You can inspect and manage your above stack with these commands:
 monk logs (-f) local/hasura/stack - Inspect logs
 monk shell     local/hasura/stack - Connect to the container's shell
 monk do        local/hasura/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Check web gui

`http://<ip>:8080/`

## Variables

The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable                         | Description              | Defaults                                                 |
|----------------------------------|--------------------------|----------------------------------------------------------|
| hasura_graphql_console           | GraphQL console enable   | true                                                     |
| hasura_graphql_dev_mode          |  GraphQL dev mode        | true                                                     |
| hasura_graphql_enabled_log_types | GraphQL log type,        | startup, http-log, webhook-log, websocket-log, query-log |
| hasura_graphql_admin_secret      | Hasura admin secret      | monk                                                     |
| database_name                    | Hasura database name     | monk                                                     |
| database_password                | Database password        | monk                                                     |
| database_user                    | Hasura database user     | monk                                                     |
| db_password                      | Hasura database password | monk                                                     |
| database_port                    | Hasura database port     | 5432                                                     |

## Stop, remove and clean up workloads and templates

```bash
monk purge hasura
```
