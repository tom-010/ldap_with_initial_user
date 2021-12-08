LDAP with initial user
======================

This repo shows how to configure LDAP with docker and 
initial users.

Inspired by [this blogpost](https://betterprogramming.pub/ldap-docker-image-with-populated-users-3a5b4d090aa4)

## Getting started

```
$ mv .env.example .env
```

add to `/etc/hosts`:
```
127.0.0.1   ldap.firmenessen.de
```
or change the `server_name` in `conf/nginx/conf.d/ldap.conf`

To start run

```
$ docker-compose up
```

and go to `ldap.firmenessen.de`

The admin-user (`Login DN`) is `cn=admin,dc=example,dc=org`.
Te password is the same as in the `.env`. In the example it is `secret?`

## Create a user in LDAP-Admin

1. Login as admin (`cn=admin,dc=example,dc=org`, `secret`)
2. Click on `dc=example,dc=org` > `Create a child entry` > `Courier Mail: Account`
3. Fill out and set the Common Name equal to User ID (isn't required, but makes some integrations easier)
4. `Create Object` > `Commit`
5. Logout
6. Login with `cn=<<Common Name>>,dc=example,dc=org` and the given password

## Developing

Remember to do `docker-compose down -v` to destroy the volumes such that the initial file
is read again. Start with `docker-compose up --build` if you changed the bootstrap.ldif