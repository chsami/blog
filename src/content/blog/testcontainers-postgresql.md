---
title: 'TestContainers in .NET with PostgreSQL and PgVector'
description: 'Lorem ipsum dolor sit amet'
pubDate: 'Dec 28 2024'
heroImage: '/28122024/banner.png'
---

## What are we solving?

How to include postgresql extension in a docker image through C# for integration tests.

## Overview


I’m using C# with the Testcontainers.PostgreSql NuGet package, which makes it easy to spin up PostgreSQL containers for integration testing. The core idea behind this setup is to ensure that each test class gets a clean, isolated database instance. This database is used to execute integration tests and is deleted afterward.

> Testcontainers for .NET is a library to support tests with throwaway instances of Docker containers for all compatible .NET Standard versions. The library is built on top of the .NET Docker remote API and provides a lightweight implementation to support your test environment in all circumstances.

## Container Configuration


Here’s how I configured the PostgreSQL container:

```
private const ushort Port = 5432;
private const string Username = "postgres";
private const string Password = "postgres";
private const string Database = "postgres";
private const string Host = "localhost";
```

```
private readonly PostgreSqlContainer _dbContainer = new PostgreSqlBuilder()
    .WithImage("pgvector/pgvector:pg16")
    .WithUsername(Username)
    .WithPassword(Password)
    .WithPortBinding(Port, true)
 .WithWaitStrategy(Wait.ForUnixContainer().UntilPortIsAvailable(Port))
    .Build();
```

Notice that I used the pgvector:pg16 Docker image, as it already comes configured with the pgvector extension.

## Adding PostgreSQL Extensions

The project requires three PostgreSQL extensions:

```
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.HasPostgresExtension("vector");  
    modelBuilder.HasPostgresExtension("btree_gin");
    modelBuilder.HasPostgresExtension("pg_trgm");
}
```

Using HasPostgresExtension ensures that EF Core manages these extensions as part of the migrations or schema setup process. The following SQL commands are automatically generated and executed:

```
CREATE EXTENSION IF NOT EXISTS "vector";
CREATE EXTENSION IF NOT EXISTS "btree_gin";
CREATE EXTENSION IF NOT EXISTS "pg_trgm";
```

### HasPostgresExtension vs UseVector

There is a distinction between HasPostgresExtension("vector") and using the extension directly through UseVector:

## Key Differences:
**HasPostgresExtension("vector")**

- Ensures that EF Core includes the extension during migrations or schema updates.
- Manages the database schema and ensures the extension is installed. 

**UseVector**

- Configures Npgsql to utilize the vector extension’s functionality, such as advanced type mappings and query capabilities.

- Enables application-level usage, like executing vector similarity queries:

`SELECT * FROM my_table ORDER BY embedding <-> query_embedding LIMIT 10;`

## Initializing the Database with Scripts

In addition to setting up extensions through EF Core, I discovered an alternative method to initialize the database in the test container using a SQL script. This is achieved with WithResourceMapping:

`WithResourceMapping("./Scripts/extensions.sql", "/docker-entrypoint-initdb.d")`

## What Does docker-entrypoint-initdb.d Do?

The docker-entrypoint-initdb.d directory allows you to provide SQL or script files that PostgreSQL executes automatically during container initialization. This approach is ideal for preloading extensions or setting up other database configurations without embedding logic directly in the code.

## Conclusion

Using EF Core with Testcontainers, I’ve set up a way to make sure each test gets a fresh and clean database. Extensions like vector, btree_gin, and pg_trgm provide useful features, and the automated setup makes it easy to get everything ready without extra work. This keeps tests reliable and maintenance straightforward.
