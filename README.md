# docker-portfwd-server-rootless

[![GitHub main workflow](https://img.shields.io/github/actions/workflow/status/dmotte/docker-portfwd-server-rootless/main.yml?branch=main&logo=github&label=main&style=flat-square)](https://github.com/dmotte/docker-portfwd-server-rootless/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/dmotte/portfwd-server-rootless?logo=docker&style=flat-square)](https://hub.docker.com/r/dmotte/portfwd-server-rootless)

This is a :whale: **Docker image** containing an **OpenSSH server** that can be used for **local port forwarding** only (rootless version). This image is almost equivalent to [dmotte/docker-portfwd-server](https://github.com/dmotte/docker-portfwd-server) but it runs as a **non-root user**.

Inspired by: https://www.golinuxcloud.com/run-sshd-as-non-root-user-without-sudo/

> :package: This image is also on **Docker Hub** as [`dmotte/portfwd-server-rootless`](https://hub.docker.com/r/dmotte/portfwd-server-rootless) and runs on **several architectures** (e.g. amd64, arm64, ...). To see the full list of supported platforms, please refer to the [`.github/workflows/main.yml`](.github/workflows/main.yml) file. If you need an architecture which is currently unsupported, feel free to open an issue.

## Usage

The first things you need are **host keys** for the OpenSSH server and an **SSH key pair** for the client to be able to connect. See the usage example of [dmotte/docker-portmap-server](https://github.com/dmotte/docker-portmap-server) for how to get them.

In general, the use of this image is very similar to [dmotte/docker-portmap-server-rootless](https://github.com/dmotte/docker-portmap-server-rootless).

In the `PERMIT_OPEN` **environment variable** you need to specify [the destinations to which port forwarding is permitted](https://man.openbsd.org/sshd_config#PermitOpen), separated by spaces. Example: `10.0.2.15:8001 10.0.2.15:8002 10.0.2.2:8003`

Finally, you can start the server:

```bash
docker run -it --rm \
    -v "$PWD/hostkeys:/ssh-host-keys" \
    -v "$PWD/myclientkey.pub:/ssh-client-keys/myclientkey.pub:ro" \
    -p2222:2222 \
    -ePERMIT_OPEN=10.0.2.15:8080 \
    dmotte/portfwd-server-rootless
```

See [dmotte/docker-portmap-server](https://github.com/dmotte/docker-portmap-server) for further details on usage; it's very similar to this one.

For a more complex example, refer to the [`docker-compose.yml`](docker-compose.yml) file.

### Environment variables

List of supported **environment variables**:

| Variable             | Required         | Description                                                      |
| -------------------- | ---------------- | ---------------------------------------------------------------- |
| `KEEPALIVE_INTERVAL` | No (default: 30) | Value for the `ClientAliveInterval` option of the OpenSSH server |
| `PERMIT_OPEN`        | Yes              | Value for the `PermitOpen` option of the OpenSSH server          |

## Development

If you want to contribute to this project, you can use the following one-liner to **rebuild the image** and bring up the **Docker-Compose stack** every time you make a change to the code:

```bash
docker-compose down && docker-compose up --build
```
