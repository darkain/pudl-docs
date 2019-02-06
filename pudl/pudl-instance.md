# pudl
## instance

### Parameters

#### $options
A key-value array of various configuration options for this `pudl` instance. Not every `pudl` driver supports
every option, as some simply wound not make any sense.

* 'username' => *(string)*<br/>
A user name used to authenticate with the given server. This is not avable in `pudlSqlite` or `pudlNull` as
authentication does not exist with these database drivers.

* 'password' => *(string)*<br/>
A password used to authenicate with the given server. This is not avable in `pudlSqlite` or `pudlNull` as
authentication does not exist with these database drivers.

* 'database' => *(string)*<br/>
Specify which database the engine should use for this `pudl` instance. For `pudlNull` this value is unused.
For `pudlSqlite` this value is the local file system path to the sqlite database file.

* 'server' => *(string)* or *[string array]*<br/>
The host name or IP address of the database server to connect to. For `pudlGalera` an array of strings is
required to specify available nodes in the database cluster.

* 'prefix' => *(string)* or *[string array]*<br/>
Allows for automatic prefixing of table names as well as find/replace table name prefixes.

* 'persistent' => *(boolean)*<br/>
If set to `true`, `pudl` will attempt to make use a persistent database connection from the available
connection pool.

* 'key' => *(string)*<br/>

* 'salt' => *(string)*<br/>

* 'timeout' => *(int)*<br/>
Connection and read timeout values.

* 'readonly' => *(boolean)*<br/>
If set to `true`, `pudl` will establish a real-only connection which precents any `INSERT`, `UPDATE`, `DELETE`
queries from executing.


#### $autoconnect
If set to `TRUE` *(default)*, a connection to the supplied data source will be made automatically.
