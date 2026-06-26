# Disclaimer
This repo has been created for a specific purpose.
The goal is to make it more easy and efficient to work with `Oracle` and `DuckDB` on a `Windows 11 64bit system`.
If you are on any other system, you are in the wrong place.
The included extension has been compiled specifically for `DuckDB 1.5.4` on `Windows 11 64bit system` and will not work on other system or version.

As the way we worked with it was through `DBeaver`, I'll base the documentation on using `DuckDB` with it, but it is not mandatory.

## DuckDB
I do not own the rights for DuckDB, therefore, I didn't change anything and only provide the official release that was download from their official website. This file has not been altered in any way.

You can retrieve the DuckDB from [DuckDB Download Page](https://duckdb.org/install/?platform=windows&environment=cli) (or [here](https://github.com/duckdb/duckdb/releases/tag/v1.5.4) if the current downloadable version is not 1.5.4 anymore). For the Oracle extension to work, you'll need to stick with the `v1.5.4`.

## Oracle extension
I do not own the rights for the Oracle extension. Only thing I did was compiling it for a specific system and version in order to provide it here. I tried to update it to enable a feature that we needed, but it didn't succeed so I'm providing the untouched one.

You can retrieve the extension from [the extension's GitHub repo](https://github.com/rinie/duckdb-oracle), which doesn't provide a compiled version at the time of writing.

# How to use
> [!NOTE]
> Documentation in progress.

Please put the `.duckdb` folder into your user profile folder `%USERPROFILE%`.