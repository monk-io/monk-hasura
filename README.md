# Hasura & Monk
This repository contains Monk.io template to deploy Hasura & Monk either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running.
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository
```bash
git clone https://github.com/Burakhan/monk-hasura
```

## Load Template
```bash
cd monk-hasura
monk load MANIFEST
```


#### Let's take a look at the themes I have installed.
```bash
foo@bar:~$ monk list monk-hasura
✔ Got the list
Type      Template               Repository  Version  Tags
runnable  monk-hasura/hasura     local       -        -
runnable  monk-hasura/hasura-db  local       -        -
group     monk-hasura/stack      local       -        -
```

## Deploy Stack
```bash
foo@bar:~$ monk run monk-hasura/stack
? Select tag to run [local/monk-hasura/stack] on: monk
✔ Starting the job: local/monk-hasura/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% hasura/graphql-engine:latest monk
✔ [================================================] 100% postgres:latest monk
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ local/monk-hasura/stack has been already running

🔩 templates/local/monk-hasura/stack
 └─🧊 Peer monk
    ├─🔩 templates/local/monk-hasura/hasura
    │  └─📦 67d75658c522844d9dd7dc06dfcb35bb-monk-hasura-hasura-monk-hasura
    │     ├─🧩 hasura/graphql-engine:latest
    │     ├─💾 /var/lib/monkd/volumes/growthbook -> /usr/local/src/app/packages/back-end/uploads
    │     └─🔌 open 16.170.252.96:8080 (0.0.0.0:8080) -> 8080
    └─🔩 templates/local/monk-hasura/hasura-db
       └─📦 a629918e0a1b6bd1632846fd0476e99a-monk-hasura-hasura-db-postgres
          ├─🧩 postgres:latest
          └─🔌 open 16.170.252.96:5432 (0.0.0.0:5432) -> 5432

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) local/monk-hasura/stack - Inspect logs
	monk shell     local/monk-hasura/stack - Connect to the container's shell
	monk do        local/monk-hasura/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```
## Check web gui

`http://16.170.252.96:8080/`



## Variables
The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable                     	| Description                               	|
|------------------------------	|-------------------------------------------	|
| hasura_graphql_console         | GraphQL console enable, Default: true 	               |
| hasura_graphql_dev_mode        | GraphQL dev mode, Default: true 	               |
| hasura_graphql_enabled_log_types| GraphQL log type, Default: startup, http-log, webhook-log, websocket-log, query-log  |
| hasura_graphql_admin_secret    | Hasura admin password, Default: monk 	               |
| database_name                  | Hasura database name, Default: monk 	               |
| database_password              | Hasura database password, Default: monk 	               |
| database_user                  | Hasura database user, Default: monk	               |
| database_port                  | Hasura database port, Default: 5432 	               |
| db_password                    | Hasura database password, Default: monk 	               |


## Stop, remove and clean up workloads and templates

```bash
monk purge -x -a
```

