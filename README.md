# PyPi Server in docker

Minimal PyPi server running in a docker container.

Expected location for an htaccess file: `/.htaccess`.

Example in Debian/Ubuntu:

```
apt-get install apache2-utils
htpasswd -cb /.htpasswd guest guest
```

Example `docker-compose.yml` file:

```
version: '3'
services:
  web:
    image: helder/pypiserver
    ports:
      - 80
    volumes:
      - ./srv:/data
      - ./htpasswd:/.htpasswd:ro

```

Add your credentials to your `.pypirc` file:

```
# ~/.pypirc
[distutils]
index-servers =
  docker

[docker]
repository: http://localhost:32815
username: guest
password: guest
```

In an app with a `setup.py`:

```
python setup.py sdist upload -r docker
```
