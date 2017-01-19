Drupal
======

[![Build Status](https://travis-ci.org/awasilyev/drupal-container.svg?branch=master)](https://travis-ci.org/awasilyev/drupal-container)

Use this role to add an apache httpd service to your [Ansible Container](https://github.com/ansible/ansible-container) project. See Role Variables below for how to configure SSL and additional parameters. 

Run the following commands to install the service:

```
# Set the working directory to your Ansible Container project root
$ cd myproject

# Install the service
$ ansible-container install awasilyev.drupal-container-role 
```

Post Install
------------

The project's `container.yml` will be updated to include an *drupal* service with the following port mappings, which you may wish to adjust:

```
ports:
  - 80:8080
  - 443:8443
```

The document root for the server is */var/www/html*. During image build, drupal version *drupal_core_version* will be installed with drush. 
Role Variables
--------------

The following variables are defined in [defaults/main.yml](./defaults/main.yml), and can be set in `main.yml`:

drupal_core_version
> Drupal version to be installed (default 8.0.x).

drupal_admin_name
> Drupal admin username (default admin)

drupal_admin_password 
> Drupal admin password (default admin)

drupal_mysql_user
drupal_mysql_password
drupal_mysql_database
> Drupal mysql parameters

APACHE_HOSTNAME
> Set the hostname (default localhost).

APACHE_SSL
> Set to True to enable SSL (defaults to False). If /etc/httpd/ssl/cert.crt and /etc/httpd/ssl/cert.key files exists, they will be used. If not, self-signed certificate are generated when the container starts.

APACHE_SSL_PROTOCOLS
> SSL protocol (default "All -SSLv2 -SSLv3")

APACHE_SSL_CIPHER_SUITE
> SSL cipher suite (default "AES256+EECDH:AES256+EDH")

APACHE_ALLOW_OVERRIDE
> AllowOverride configuration option (default "All")

APACHE_VHOST_OPTIONS
> Options vhost configuration option (default "Indexes FollowSymLinks")

APACHE_DEFAULT_CHARSET
> Apache default charset (default "UTF-8")

APACHE_EXTRA_PARAMETERS
> List of additional parameters for vhost (default []), for example:
```
APACHE_EXTRA_PARAMETERS:
  - 'RewriteCond %{HTTP_HOST} !^www\. [NC]'
  - 'RewriteRule ^(.*)$ http://www.%{HTTP_HOST}%{REQUEST_URI} [R=301,L]'
```

Dependencies
------------

None.

License
-------

MIT/BSD

Author Information
------------------

[@awasilyev](https://github.com/awasilyev)
