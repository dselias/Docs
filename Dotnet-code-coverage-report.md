# Code coverage report

When using coverlet to run unit tests inside the project, you can generate a report with reportgenerator using the following commands.

### Install the necessary packages

`dotnet tool install -g coverlet.console`\
`dotnet tool install -g dotnet-reportgenerator-globaltool`

### Generate report json file

`dotnet test /p:CollectCoverage=true /p:CoverletOutputFormat=cobertura`

### Generate HTML report

`reportgenerator "-reports:./*/coverage.cobertura.xml" "-targetdir:./.idea/coverage-report" "-reporttypes:Html"`
