# Upgrading JupyterHub and its database

From time to time, you may wish to upgrade JupyterHub to take advantage
of new releases. Much of this process is automated using scripts,
such as those generated by alembic for database upgrades. Before upgrading a
JupyterHub deployment, it's critical to backup your data and configurations
before shutting down the JupyterHub process and server.

## Databases: SQLite (default) or RDBMS (PostgreSQL, MySQL)

The default database for JupyterHub is a [SQLite](https://sqlite.org) database.
We have chosen SQLite as JupyterHub's default for its lightweight simplicity
in certain uses such as testing, small deployments and workshops.

When running a long term deployment or a production system, we recommend using
a traditional RDBMS database, such as [PostgreSQL](https://www.postgresql.org)
or [MySQL](https://www.mysql.com), that supports the SQL `ALTER TABLE`
statement.

For production systems, SQLite has some disadvantages when used with JupyterHub:

- `upgrade-db` may not work, and you may need to start with a fresh database
- `downgrade-db` **will not** work if you want to rollback to an earlier
  version, so backup the `jupyterhub.sqlite` file before upgrading

The sqlite documentation provides a helpful page about [when to use sqlite and
where traditional RDBMS may be a better choice](https://sqlite.org/whentouse.html).

## The upgrade process

Four fundamental process steps are needed when upgrading JupyterHub and its
database:

1. Backup JupyterHub database
2. Backup JupyterHub configuration file
3. Shutdown the Hub
4. Upgrade JupyterHub
5. Upgrade the database using run `jupyterhub upgrade-db`

Let's take a closer look at each step in the upgrade process as well as some
additional information about JupyterHub databases.

### Backup JupyterHub database

To prevent unintended loss of data or configuration information, you should
back up the JupyterHub database (the default SQLite database or a RDBMS
database using PostgreSQL, MySQL, or others supported by SQLAlchemy):

- If using the default SQLite database, back up the `jupyterhub.sqlite`
  database.
- If using an RDBMS database such as PostgreSQL, MySQL, or other supported by
  SQLAlchemy, back up the JupyterHub database.

Losing the Hub database is often not a big deal. Information that resides only
in the Hub database includes:

- active login tokens (user cookies, service tokens)
- users added via GitHub UI, instead of config files
- info about running servers

If the following conditions are true, you should be fine clearing the Hub
database and starting over:

- users specified in config file
- user servers are stopped during upgrade
- don't mind causing users to login again after upgrade

### Backup JupyterHub configuration file

Additionally, backing up your configuration file, `jupyterhub_config.py`, to
a secure location.

### Shutdown JupyterHub

Prior to shutting down JupyterHub, you should notify the Hub users of the
scheduled downtime. This gives users the opportunity to finish any outstanding
work in process.

Next, shutdown the JupyterHub service.

### Upgrade JupyterHub

Follow directions that correspond to your package manager, `pip` or `conda`,
for the new JupyterHub release. These directions will guide you to the
specific command. In general, `pip install -U jupyterhub` or
`conda upgrade jupyterhub`

### Upgrade JupyterHub databases

To run the upgrade process for JupyterHub databases, enter:

```
jupyterhub upgrade-db
```

## Upgrade checklist

1. Backup JupyterHub database:
    - `jupyterhub.sqlite` when using the default sqlite database
    - Your JupyterHub database when using an RDBMS 
2. Backup JupyterHub configuration file: `jupyterhub_config.py`
3. Shutdown the Hub
4. Upgrade JupyterHub
    - `pip install -U jupyterhub` when using `pip`
    - `conda upgrade jupyterhub` when using `conda`
5. Upgrade the database using run `jupyterhub upgrade-db`
