* _NOTE: This is a "work in progress" document and will take a few weeks to be fully filled out. Most things listed in this document will become full pages of their own and linked here in the very near future._

# PUDL Documentation

## What is PUDL
PUDL stands for "_PHP Universal Database Library_" and can simply be described as "_PDO on crack._" PUDL provides a straightforward, simple, and standardized API for connecting to various database engines using the available PHP extensions transparently. Additionally, PUDL provides APIs for automatically generating SQL queries as well as processing the resulting data.

## Getting Started

### Supported Database Engines and PHP Extensions
Class		| Support		| Information
------------|---------------|------------
pudl		| Full			| The core shared API
pudlNull	| Full			| Think _/dev/null_, no connection made, calls return default value
pudlMySql	| Full			| Legacy MySQL (_deprecated in PHP 5.5.0, removed in PHP 7.0.0_)
pudlMySqli	| Full			| Modern MySQL, MariaDB, and Percona
pudlGalera	| Full			| MySqli interface extended with Galera multi-master clustering
pudlMsSql	| Partial		| Legacy Microsoft SQL Server (_removed in PHP 7.0.0_)
pudlSqlSrv	| Partial		| Modern Microsoft SQL Server
pudlPgSql	| Partial		| PostgreSQL
pudlSqlite	| Partial		| Local Sqlite3 file
pudlOdbc	| Partial		| Open Database Connectivity
pudlPdo		| Partial		| PHP's built in PDO
pudlShell	| Experimental	| JSON API accessed via piped connections on a local shell
pudlWeb		| Experimental	| JSON API accessed via HTTP(s)

### Basic Queries



## API Documentation


### Classes


### Constants
Prefix								| Information
------------------------------------|------------
[PUDL_](constants/pudl.md)			| Main PUDL constants
[GALERA_](constants/galera.md)		| Galera cluster status


### Interfaces
Interface							| Information
------------------------------------|------------
[pudlData](pudlData)				| Used internally to identify specific data structures
[pudlHelper](pudlHelper)			| Used internally to identify special PUDL related classes
[pudlId](pudlId)					| Allows an object to be passed into an Id() function as a value
[pudlValue](pudlValue)				| Used internally to identify special PUDL values


### Object-Relational Mapping (ORM)
Class								| Information
------------------------------------|------------
[pudlObject](pudlObject)			| A basic object that acts like a PHP Array
[pudlOrm](pudlOrm)					| A hybrid between pudlObject and the main PUDL interface
[pudlCollection](pudlCollection)	| A collection of pudlOrm objects


### Importing / Exporting
* pudlImport
* pudlImportCsv
* pudlImportExcel
* pudlExportExcel
