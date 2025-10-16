# tserve

tserve, or tiny server is a compose file for setting up a lightweight static HTTP server using BusyBox Linux.

While ultra-small images, like [Lipan's](https://lipanski.com/posts/smallest-docker-image-static-website) do exist, this compose file uses the Docker library BusyBox image and configures it using the compose specification to maximise architecture support and CDN availability.

## Usage
Download the `compose.yml` file, add your static files to the `./www` directory and lauch the image with Docker or Podman!

### Compose example

You can uncomment the mount for `httpd.conf` if you wish to customise how the `httpd` binary operates, have a look at [Yorston's blog](https://frippery.org/busybox/httpd.html) for for information

```yml
services:
  serve:
    image: docker.io/library/busybox:latest
    restart: unless-stopped
    volumes:
      - ./www:/www:ro
      # - ./httpd.conf:/etc/httpd.conf:ro
    ports:
      - 80:80
    command: httpd -f -v -h /www
    healthcheck:
      test: wget --spider http://localhost
```
