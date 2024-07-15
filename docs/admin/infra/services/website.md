# Web services

## nucleoid.xyz

The website is served as a static site by apache2 from `/var/www/nucleoid.xyz`. It's build automatically by GitHub Actions, so you just need to `sudo git pull` from that folder to update the site once it has built.

## maven.nucleoid.xyz and build.nucleoid.xyz

These are both also just "static" sites running under `apache2` (well all our web stuff goes through here, but most of them are just proxied).

The maven repository is deployed to using sftp logging in as the `maven` user (ask on Discord for the password if you need to set something up to deploy there).

The build site is just a symlink to the exports directory of the building server.

Both are using [h5ai](https://github.com/lrsjng/h5ai) for a nicer looking static file browser.

## stats.nucleoid.xyz

Running under `docker-compose` from `/home/minecraft/services/stats`.

## api.nucleoid.xyz

Is reverse proxied through to several services:

- [backend](backend.md)
- [mitosis](misc.md#mitosis-and-face-api)
- [face-api](misc.md#mitosis-and-face-api)
