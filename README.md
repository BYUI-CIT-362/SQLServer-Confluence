# SQL Server Confluence
This is just a generic SQL Server container that was created for kubernetes. To run locally:

`docker build . -t sqlserver`
`docker run -p 1433:1433 --memory="6g" --env-file ./env.list sqlserver`

Sample JDBC Connection String:

`jdbc:sqlserver://localhost;databaseName=confluence;`

Queries you will need to run:

`create database confluence`

`alter database confluence collate SQL_Latin1_General_CP1_CS_AS;`

`alter database confluence set READ_COMMITTED_SNAPSHOT ON WITH ROLLBACK IMMEDIATE;`

Here is a snapshot of usage during setup of the confluence database, where brave_yalow is the confluence container and blissful_taussig is the database pod. Notice the database uses multiple cores, probably 3-4 during install. They both are doing fine with 2 GB of memory at the setup phase, that will vary with later usage.

```
CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
2c39fdbb2d52        brave_yalow         1.65%               1.485GiB / 1.943GiB   76.43%              400kB / 1.48MB      0B / 0B             99
3c881ece6a57        blissful_taussig    23.23%              156.4MiB / 1.943GiB   7.86%               1.3MB / 524kB       0B / 0B             133
```

