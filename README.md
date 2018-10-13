* _NOTE: This is a "work in progress" document and will take a few weeks to be fully filled out. Most things listed in this document will become full pages of their own and linked here in the very near future._

# PUDL Documentation

## What is PUDL
PUDL stands for "_PHP Universal Database Library_" and can simply be described as "_PDO on crack._" PUDL provides a straightforward, simple, and standardized API for connecting to various database engines using the available PHP extensions transparently. Additionally, PUDL provides APIs for automatically generating SQL queries as well as processing the resulting data.

## Getting Started

### Creating an instance of the initial PUDL object
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
pudlShell	| Experimental	| JSON API accessed via piped connections on a local shell
pudlWeb		| Experimental	| JSON API accessed via HTTP(s)
pudlPdo		| Partial		| PHP's built in PDO

### Basic Queries

## API Documentation
### Classes

### Interfaces
* pudlData
* pudlHelper
* pudlId
* pudlValue

### Constants
* PUDL_ main PUDL constants
* GALERA_ constants used for Galera cluster status

### Importing / Exporting
* pudlImport
* pudlImportCsv
* pudlImportExcel
* pudlExportExcel

## Object-Relational Mapping (ORM)
* [pudlObject](pudlObject) - a basic object that acts like a PHP Array
* [pudlOrm](pudlOrm) - a hybrid between pudlObject and the main PUDL interface
* [pudlCollection](pudlCollection) - a collection of pudlOrm objects
