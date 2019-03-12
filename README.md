About
-------------------------------

Connect to and use a remote database over an SSH tunnel in Django.

Installation
-------------------------------

`pip install django-dbtunnel`

Example Usage
-------------------------------

Usage is very simple by with the built-in context manager `database_tunnel(database, use_ssh_config=False)`. After starting the tunnel simply use query filters as you normally would with the using() method matching the name of the remote database you are connected to.

```python
from dbtunnel import database_tunnel
with database_tunnel('remote_db'):
	obj = SomeModel.objects.using('remote_db').filter(x=1)
```

Also available is the non-context manager methods:

* `start_tunnel(database, use_ssh_config=False)`
* `stop_tunnel(database)`

Where `database` is the keyname of the database to use from your Django DATABASES setting and `use_ssh_config` will apply any settings provided in your ~/.ssh/config file.

Then some settings like:

```python
DATABASES = {
	'default': {
	'ENGINE': 'django.db.backends.postgresql_psycopg2',
    	'NAME': 'database_name',
    	'USER': 'username',
    	'PASSWORD': 'password',
    	'HOST': 'ip_address_of_server',
    	'PORT': '5432',
    	'REMOTE_HOST': 'ip_address_of_server',
    	'TUNNEL_USER': 'ssh_username',
    	'TUNNEL_PASSWORD': 'ssh_password',
    	'TUNNEL_HOST': 'ip_address_of_server'
    }
}
```

You may also need to set up listen_addresses in /etc/postgresql/9.5/main/postgresql.conf to accept certain ip addresses or just all addresses with listen_addresses = '*'

Also in /etc/postgresql/9.5/main/ph_.conf and add a line at the bottom e.g. host all all 0.0.0.0/0 md5 for access for all who have the login credentials.

License
-------------------------------

MIT
