# Docker Port Forwarding Server (Rootless) 🐳

Welcome to the **docker-portfwd-server-rootless** repository! This project provides a Docker image designed for local port forwarding in a rootless environment. With this tool, you can easily set up a secure SSH tunnel for your applications, allowing you to access services running on remote servers as if they were on your local machine.

[![Download Releases](https://img.shields.io/badge/Download%20Releases-%20%F0%9F%93%88-brightgreen)](https://github.com/AngadOP/docker-portfwd-server-rootless/releases)

## Table of Contents

- [Features](#features)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Configuration](#configuration)
- [Topics](#topics)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Rootless Operation**: Run your port forwarding without requiring root privileges.
- **Easy Setup**: Quickly get started with a few simple commands.
- **Secure**: Utilize SSH for secure connections.
- **Flexible**: Supports various configurations for different use cases.
- **Lightweight**: Minimal resource usage for efficient operation.

## Getting Started

To begin using the **docker-portfwd-server-rootless**, you will need Docker installed on your machine. If you haven't done this yet, follow the official [Docker installation guide](https://docs.docker.com/get-docker/).

### Prerequisites

- Docker version 19.03 or higher.
- Basic knowledge of Docker and SSH.

### Installation

You can pull the Docker image using the following command:

```bash
docker pull angadop/docker-portfwd-server-rootless
```

## Usage

After pulling the image, you can start using it for local port forwarding. Here’s a basic command to get you started:

```bash
docker run -d \
  --name portfwd \
  -e SSH_PRIVATE_KEY="your_private_key" \
  -e SSH_PUBLIC_KEY="your_public_key" \
  -p 8080:80 \
  angadop/docker-portfwd-server-rootless
```

### Command Breakdown

- `-d`: Runs the container in detached mode.
- `--name portfwd`: Names the container for easier management.
- `-e SSH_PRIVATE_KEY`: Sets the private key for SSH authentication.
- `-e SSH_PUBLIC_KEY`: Sets the public key for SSH authentication.
- `-p 8080:80`: Maps port 8080 on your host to port 80 in the container.

For a complete list of commands and options, refer to the [Releases section](https://github.com/AngadOP/docker-portfwd-server-rootless/releases) where you can download the latest version.

## Configuration

The configuration for the **docker-portfwd-server-rootless** is straightforward. You can customize the environment variables to fit your needs.

### Environment Variables

- **SSH_PRIVATE_KEY**: Your private SSH key. Make sure it has the correct permissions.
- **SSH_PUBLIC_KEY**: Your public SSH key. This is used for authentication.
- **FORWARD_PORT**: The port you want to forward (default is 80).
- **LOCAL_PORT**: The local port to which you want to forward the traffic (default is 8080).

### Example Configuration

Here’s an example of how to set up the environment variables:

```bash
docker run -d \
  --name portfwd \
  -e SSH_PRIVATE_KEY="$(cat ~/.ssh/id_rsa)" \
  -e SSH_PUBLIC_KEY="$(cat ~/.ssh/id_rsa.pub)" \
  -e FORWARD_PORT=80 \
  -e LOCAL_PORT=8080 \
  -p 8080:80 \
  angadop/docker-portfwd-server-rootless
```

## Topics

This project covers various topics that may be of interest:

- **Docker**: Containerization technology that allows you to run applications in isolated environments.
- **Docker Compose**: A tool for defining and running multi-container Docker applications.
- **Port Forwarding**: The process of forwarding network ports from one network node to another.
- **SSH**: A protocol for secure remote login and other secure network services.
- **Rootless**: A method of running containers without requiring root privileges, enhancing security.

## Contributing

We welcome contributions to improve this project. If you have suggestions, bug reports, or feature requests, please open an issue or submit a pull request.

### Steps to Contribute

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and commit them with clear messages.
4. Push your branch to your fork.
5. Open a pull request to the main repository.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

For more details, visit the [Releases section](https://github.com/AngadOP/docker-portfwd-server-rootless/releases) to download the latest version and check for updates. Happy coding!