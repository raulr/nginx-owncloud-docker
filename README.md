
The [official ownCloud image](https://hub.docker.com/r/library/owncloud/) has a PHP-FPM variant, but it still needs a web server to handle HTTP requests. This image provides an Nginx server ready to use as a `owncloud:fpm` front-end.

The Nginx configuration in this image is based on the guidelines given by the [ownCloud Documentation](https://doc.owncloud.org/server/8.2/admin_manual/installation/nginx_configuration.html).

### How to Use This Image

    $ docker run --name some-nginx --link some-owncloud:owncloud --volumes-from some-owncloud -d -p 8080:80 raulr/nginx-owncloud

### ... via [`docker-compose`](https://github.com/docker/compose)

Example `docker-compose.yml`:

```yaml
owncloud:
  image: owncloud:fpm
nginx:
  image: raulr/nginx-owncloud
  links:
   - owncloud
  volumes_from:
   - owncloud
  ports:
   - "8080:80"
```

Run `docker-compose up`, wait for it to initialize completely, and visit `http://localhost:8080` or `http://host-ip:8080`.
