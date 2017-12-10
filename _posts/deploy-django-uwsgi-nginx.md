# NGINX Configurations

File `nginx.conf`
```
# mysite_nginx.conf

# the upstream component nginx needs to connect to
upstream django {
    # server unix:///path/to/your/mysite/mysite.sock; # for a file socket
    server 127.0.0.1:8000; # for a web port socket (we'll use this first)
}

# configuration of the server
server {
    # the port your site will be served on
    listen      80;
    # the domain name it will serve for
    server_name 127.0.0.1; # substitute your machine's IP address or FQDN
    charset     utf-8;

    # max upload size
    client_max_body_size 75M;   # adjust to taste

    # Django media
    location /media  {
        alias /path/to/django/project/media;  # your Django project's media files - amend as required
    }

    location /static {
        alias /path/to/django/project/staticroot; # your Django project's static files - amend as required
    }

    # Finally, send all non-media requests to the Django server.
    location / {
        uwsgi_pass  django;
        include     /path/to/djagno/project/uwsgi_params; # the uwsgi_params file you installed
    }
}

```

# uWSGI configuration
file `uwsgi.ini`

```
# mysite_uwsgi.ini file
[uwsgi]

# Django-related settings
# the base directory (full path)
chdir           = /path/to/django/project
env = DJANGO_SETTINGS_MODULE=your_project.settings
# Django's wsgi file
module          = your_project.wsgi
# the virtualenv (full path)
home            = /root/.pyenv/versions/cboxpro

# process-related settings
master          = true
processes       = 5 # maximum number of worker processes
# the socket (use the full path to be safe
socket          = 127.0.0.1:8000
max-requests = 5000  # respawn processes after serving 5000 req
# clear environment on exit
vacuum          = true

```

# Run uWSGI

```bash
$ uwsgi --ini uwsgi.ini
```

# Run Nginx proxy server

```bash
$ sudo service nginx start
```
