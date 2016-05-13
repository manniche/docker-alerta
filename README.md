
alerta
======

Alerta monitoring tool for consolidated view of alerts

Installation
------------

This docker image runs a mongo database in a container alongside the
alerta-web container.

Start up the mongo container and the web-interface with

    $ docker-compose up

The API endpoint is at:

    http://<docker>:<port>/api

Browse to the alerta console at:

    http://<docker>:<port>/

To check running processes and tail the application and web server logs:

    $ docker top alerta-web
    $ docker-compose logs -f

Configuration
-------------

To make it easy to get going with alerta on docker quickly, the default image will use Basic Auth for user logins.

To allow users to login using Google OAuth, go to the [Google Developer Console][1] and create a new client ID for a web application. Then set the `CLIENT_ID` and `CLIENT_SECRET` environment variables in the `alerta-web.env` file as follows:

    CLIENT_ID=379647311730-6tfdcopl5fodke08el52nnoj3x8mpl3.apps.googleusercontent.com
    CLIENT_SECRET=UpJxs02c_bx9GlI3X8MPL3-p

This will allow users to login but will only make it optional. To enforce users to login additionally set the `AUTH_REQUIRED` environment variable to `True` in the `alerta-web.env` file:

    AUTH_REQUIRED=True

To restrict logins to a certain email domain set the `ALLOWED_EMAIL_DOMAIN` environment variable as follows:

    ALLOWED_EMAIL_DOMAIN=example.com

GitHub and GitLab can also be used as the OAuth2 providers by setting the `PROVIDER` environment variable to `github` and `gitlab` respectively.

Command-line Tool
-----------------

A command-line tool for alerta is available. To install it run:

    $ pip install alerta

Configuration file `$HOME/.alerta.conf`:

    [DEFAULT]
    endpoint = http://<docker>:<port>/api

If authentication is enabled (ie. `AUTH_REQUIRED` is `True`), then create a new API key in the alerta console and add the key to the configuration file. For example:

    [DEFAULT]
    endpoint = ...
    key = 4nHAAslsGjLQ9P0QxmAlKIapLTSDfEfMDSy8BT+0

Further Reading
---------------

More information about alerta can be found at http://docs.alerta.io

License
-------

Copyright (c) 2014-2016 Nick Satterly. Available under the MIT License.

[1]: <https://console.developers.google.com> "Google Developer Console"
