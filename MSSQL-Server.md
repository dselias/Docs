# MSSQL Server setup on Linux for Dotnet development

- Create a DB container: `docker run --name <container_name> -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=T0orT0or" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2022-latest`
- Create the DB using SQL: `CREATE DATABASE <DB_name>` (this needs to be done because the dotnet migrator user doesn't have permissions to create databases)
- Assign the right connectionstring in appsettings: `"Server=localhost;Database=<DB_name>;User=sa;Password=T0orT0or;MultipleActiveResultSets=True;TrustServerCertificate=true"`
- Run migrations
