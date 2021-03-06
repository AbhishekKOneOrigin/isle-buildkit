# Crayfish

Docker image for [Crayfish] version 1.1.1.

Acts as base Docker image for Crayfish based micro-services. It is not meant to
be run on its own.

## Dependencies

Requires `islandora/nginx` docker image to build. Please refer to the
[Nginx Image README](../nginx/README.md) for additional information including
additional settings, volumes, ports, etc.

## Ports

| Port | Description |
| :--- | :---------- |
| 8000 | HTTP        |

## Settings

> N.B. For all of the settings below images that descend from
> ``islandora/crayfish`` will apply prefix to every setting. So for example
> `JWT_ADMIN_TOKEN` would become `GEMINI_JWT_ADMIN_TOKEN` this is to allow for
> different settings on a per-service basis.

| Environment Variable | Confd Key        | Default                                        | Description                                                           |
| :------------------- | :--------------- | :--------------------------------------------- | :-------------------------------------------------------------------- |
| JWT_ADMIN_TOKEN      | /jwt/admin/token | islandora                                      | JWT Token                                                             |
| JWT_PUBLIC_KEY       | /jwt/public/key  | See rootfs/etc/confd/templates/public.key.tmpl | The public key must match the public key used in the Drupal container |

[Crayfish]: https://github.com/Islandora/Crayfish/tree/main
