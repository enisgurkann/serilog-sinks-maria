# Serilog.Sinks.MariaDB
Serilog sink that writes to Maria database.

## Getting started

Install [Serilog.Sinks.MariaDB](https://www.nuget.org/packages/Serilog.Sinks.MariaDB) from NuGet

```PowerShell
Install-Package Serilog.Sinks.MariaDB
```

Configure logger by calling WriteTo.MariaDB

```C#
var logger = new LoggerConfiguration()
    .WriteTo.MariaDB("server=127.0.0.1;uid=user;pwd=password;database=diagnostics;")
    .CreateLogger();

logger.Information("This informational message will be written to MariaDB database");
```

## XML <appSettings> configuration

To use the rolling file sink with the [Serilog.Settings.AppSettings](https://www.nuget.org/packages/Serilog.Settings.AppSettings) package, first install that package if you haven't already done so:

```PowerShell
Install-Package Serilog.Settings.AppSettings
```
In your code, call `ReadFrom.AppSettings()`

```C#
var logger = new LoggerConfiguration()
    .ReadFrom.AppSettings()
    .CreateLogger();
```

In your application's App.config or Web.config file, specify the MariaDB sink assembly and required **connectionString** under the `<appSettings>` node:

```XML
<appSettings>
    <add key="serilog:using:MariaDB" value="Serilog.Sinks.MariaDB"/>
    <add key="serilog:write-to:MariaDB.connectionString" value="..."/>
    <add key="serilog:write-to:MariaDB.tableName" value="Logs"/>
    <add key="serilog:write-to:MariaDB.storeTimestampInUtc" value="true"/>
</appSettings>    
```

>Note:
This sink version 4.1 has breaking changes. It expects an additional column `Template` of type Template `TEXT` in log table.
It is recommended to add this column manually or delete existing table so that it can be recreated correctly. 

[![Build status](https://ci.appveyor.com/api/projects/status/tse5g3weca5nmky3?svg=true)](https://ci.appveyor.com/project/SaleemMirza/serilog-sinks-mariadb)

