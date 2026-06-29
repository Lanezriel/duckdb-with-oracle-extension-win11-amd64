- [Disclaimer](#disclaimer)
    - [DuckDB](#duckdb)
    - [Oracle extension](#oracle-extension)
    - [DBeaver](#dbeaver)
- [How to use](#how-to-use)
    <ol type="1">
      <li><a href="#1-where-should-i-place-the-files">Where should I place the files?</a></li>
      <li><a href="#2-configure-you-environment-variable-path">Configure your environment variable (PATH)</a></li>
      <li><a href="#3-create-the-persistent-duckdb">Create the persistent DuckDB</a></li>
      <li><a href="#4-install-mysql-extension">Install MySQL extension</a></li>
      <li><a href="#5-install-dbeaver">Install DBeaver</a></li>
      <li><a href="#6-create-a-duckdb-connection">Create a DuckDB connection</a></li>
      <li><a href="#7-install-oracle-client">Install Oracle client</a></li>
      <li><a href="#8-configure-dbeavers-bootstrap-queries">Configure DBeaver's Bootstrap Queries</a></li>
      <li><a href="#9-use-oracle_attach-function-to-access-oracle-db-tables">Use oracle_attach() function to access Oracle DB tables</a></li>
    </ol>

# Disclaimer
This repo has been created for a specific purpose.
The goal is to make it more easy and efficient to work with `Oracle` and `DuckDB` on a `Windows 11 64bit system`.
If you are on any other system, you are in the wrong place.
The included extension has been compiled specifically for `DuckDB 1.5.4` on `Windows 11 64bit system` and will not work on other system or version.

As the way we worked with it was through `DBeaver`, I'll base the documentation on using `DuckDB` with it, but it is not mandatory.

## DuckDB
I do not own the rights for DuckDB, therefore, I didn't change anything and only provide the official release that was downloaded from their official website. This file has not been altered in any way.

You can retrieve the DuckDB from [DuckDB Download Page](https://duckdb.org/install/?platform=windows&environment=cli) (or [here](https://github.com/duckdb/duckdb/releases/tag/v1.5.4) if the current downloadable version is not 1.5.4 anymore). For the Oracle extension to work, you'll need to stick with the `v1.5.4`.

## Oracle extension
I do not own the rights for the Oracle extension. Only thing I did was compiling it for a specific system and version in order to provide it here. I tried to update it to enable a feature that we needed, but it didn't succeed so I'm providing the untouched one.

You can retrieve the extension from [the extension's GitHub repo](https://github.com/rinie/duckdb-oracle), which doesn't provide a compiled version at the time of writing.

## DBeaver
I will not provide it myself.  
You can download it [there](https://dbeaver.io/download/) if necessary, or inside the `Software Center` from your company if there is one.

# How to use
## 1. Where should I place the files?
Start by placing the `.duckdb` folder into your user profile folder, which you can access by typing `%USERPROFILE%` top-center path bar (or usually with `C:\Users\USERNAME\`), so you can have these 2 paths:
- C:\Users\USERNAME\.duckdb\duckdb.exe
- C:\Users\USERNAME\.duckdb\extensions\v1.5.4\windows_amd64\oracle.duckdb_extension

## 2. Configure your environment variable (PATH)
Push on the `Windows key` on your keyboard (or click on the `Windows Logo` on the taskbar), then type `env` and you should be able to find `Edit environment variables for your account`.  
Click on it.

On the opened window, in the upper part (called `User variables for USERNAME`), find `Path` and double click on it.  
Then click on the `New` button from the right and enter `C:\Users\USERNAME\.duckdb`.  
This will make your terminal able to directly find duckDB so you won't need to type the whole path to the exe file.

Now you can just type `duckdb` in a new terminal and it should work.

## 3. Create the persistent DuckDB
On a terminal, launch `DuckDB` with this command: `duckdb .\DBNAMEYOUWANT.duckdb`.  
This will create a file on your current working directory. You'll need that file to use DuckDB with DBeaver.

## 4. Install MySQL extension
If you also need to work with MySQL, let's install that extension (not provided in this repo).
If you're not in DuckDB anymore, relaunch it with the previous command, then type `INSTALL mysql;` and press `ENTER`.  
This should install the extension.

If you are having trouble installing it, by being behing a company proxy for example, there are 2 possibilities.
- Try to set the proxy informations so it can get through it by using these 3 statements:
    > SET http_proxy = 'http://YOUR_PROXY_ADDRESS:PORT';  
    > SET http_proxy_username = 'USERNAME';  
    > SET http_proxy_password = 'YOUR_PASSWORD';
- Connect to the internet using an other connection. You can share your phone's connection, for example.

## 5. Install DBeaver
> [!NOTE]
> If you want to use the DuckDB CLI, you can skip the next part.  
> But remember that you'll need to understand what's done inside DBeaver in order to adapt it for your CLI usage.  
> This should not be that hard.

If you are behind a company network, please check your company's `Software Center` first.  
If it is available there, you should use the one your company provides (installation should be automatic from there).

If not, go to the official [DBeaver Download Page](https://dbeaver.io/download/), download it and install it.

## 6. Create a DuckDB connection
> [!WARNING]
> For this part, you might have trouble installing the drivers from behind a company network.  
> If that's the case, you will need to use an external connection (like sharing your phone's connection)  
> For simplicity, we advise you to be on external network for this part, this will be easier.

Once installed, open `DBeaver` and create a new connection.  
Select `DuckDB` and click on the `Browse...` button on the right of the `path field`, select your `DuckDB file` (created previously), then click on `Test Connection...`.

> [!IMPORTANT]
> At this point, you might encounter an issue for finding the drivers.  
> If you have a message that looks like `org.duckdb...........RELEASE not found`, you'll need to use a simple trick to make the driver discoverable.  
> Go to `Window` dropdown on top of the application and select `Preferences`.  
> Append `Connections` then `Drivers` and select `Maven`.  
> On the right panel, click on `Restore Defaults` then `Apply and Close`.  
> Now if you try to find the driver again, it should show up.

You'll be asked to install the driver for `DuckDB` and you should see a line about the JDBC driver with information about the version (`v1.5.4`).  
Click on `Download`.

Once installed, you should see a confirmation window saying it can connect to the `DuckDB`.  
If so, click on `Finish` and you'll be able to see your `DuckDB` on the left panel list, named with the `DuckDB file name` (you can also rename it if you want).

Test the connection by right clicking on it, selecting `SQL Editor` and `New SQL script`.  
There you can test with:
> `SELECT 'Ready to fly' as first_duckdb_query;`

You should directly see the result without error.

## 7. Install Oracle client
> [!NOTE]
> I'm not pretty sure the oracle extension required this, but I already had one installed so I couldn't check.  
> I guess it's still better to have it, just in case.

If you want to connect to Oracle, you should have an Oracle client on your machine, like the `Oracle Client 19c 64bits (19.28.0.0)` for example.

In order to get the Oracle client, if you are behind a company network, please check the `Software Center` first (if your company has one).  
If there is an Oracle client, then use the one provided by your company.  
If not, you can download it on the [Official Oracle Instant Client Download Page](https://www.oracle.com/database/technologies/instant-client/downloads.html).

Install it, and you should be alright.

## 8. Configure DBeaver's Bootstrap Queries
In order to not have to execute statements every time you connect to your `DuckDB`, let's create `Bootstrap Queries`.  
These queries will automatically run when you initiate a connection to you `DuckDB`.

> [!CAUTION]
> If one of your `Bootstrap Queries` is not working, you won't be provided with any error message or any tip on what's not working.  
> If something seems wrong, remove some and retry.  
> Basically, you should add them one by one and test it every time you add one so you'll know exactly which statement is failing.

Right click on the `DuckDB` on the left panel of `DBeaver`, then select `Edit Connection`.  
On the new window, append `Connection settings` on the left panel and click on `Initialization`.  
Click on the `Configure ...` button on the right of `Bootstrap queries`.  
Add new entries like so:
- `LOAD oracle;`
- `LOAD mysql;`
- `ATTACH 'host=MYSQL_HOST port=MYSQL_PORT user=DB_USER password=DB_USER_PASSWORD database=DB_NAME' AS WHATEVER_NAME_YOU_WANT (TYPE mysql);`

As you can see, we didn't add a statement to attack Oracle DB.  
The provided extension can do the same ([refer to the extension doc itself for this](https://github.com/rinie/duckdb-oracle)) but we wont.  
Reason is simple, we need to access schemas that we do not own but where we have, at least, reading rights.  
Unfortunately, the `ATTACH` method of the extension is only able to show you the schemas that you own, so we'll use a specific function that is not documented at the time of writing: `oracle_attach()`.

## 9. Use oracle_attach() function to access Oracle DB tables
This function will create views for all the tables of the specified schema, and you'll be able to query these tables in your cross queries.  
It will also need to be done only once as the views are stored in the `DuckDB` and reloaded everytime.  
In the DBeaver script window (where you tested the DuckDB connection previously), enter the following query:
```
SELECT *
FROM oracle_attach(
    'USERNAME/PASSWORD@(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=ORACLE_DB_HOST)(PORT=ORACLE_DB_PORT))(CONNECT_DATA=(SERVICE_NAME=ORACLE_DB_SERVICE_NAME)))',
    source_schema = 'ORACLE_DB_SCHEMA_YOU_WANT_TO_GET_THE_TABLES',
    sink_schema = 'YOUR_DUCKDB_SCHEMA_WHERE_YOU_WANT_TO_PUT_THE_CREATED_VIEWS',
    overwrite = true,
    filter_pushdown = true
);
```

> [!NOTE]
> This query can take a few minutes as it needs to generate the views for every table in the Oracle DB Schema.

As you can see, we used a `full descriptor` for the connection instead of the usual `connection strings`.  
We decided to go that way in order to `avoid any trouble with the TNS Names`.  
With the way we did, it should work whether you have tnsnames.ora or not.  
We also advise you to not `set a TNS_ADMIN` environment variable with a tnsnames.ora. If you do so, it will check for EVERY CONNECTION and will `slow your process down`.