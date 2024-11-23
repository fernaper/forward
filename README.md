# Forward

`Forward` is a Bash script that facilitates port redirection and SSH tunneling with optional Docker container integration. It simplifies redirecting ports between local and remote servers and supports exposing services publicly using localhost.run.

## Features

- Redirect ports between local and remote servers.
- Seamless integration with Docker containers to redirect container ports.
- Publicly expose local ports via localhost.run.
- Auto-completion for easy usage with `-s`, `-p`, `-P`, and `-d` options.

## Usage

```bash
forward [-s user@remote_server] -p local_port:external_port [-P] [-d container_name]
```

### Options

- `-s user@remote_server`  
  Specify the remote server for SSH tunneling. Defaults to `localhost`.

- `-p local_port:external_port`  
  Define the local and external ports for redirection. Both are required unless using the `-d` option.

- `-P`  
  Expose the local port publicly using localhost.run.

- `-d container_name`  
  Redirect ports from a Docker container. Automatically fetches the container's IP address.

## Installation

1. Save the script as `forward`.
2. Make it executable:
   ```bash
   chmod +x forward
   ```
3. Source it for autocompletion:
   ```bash
   source forward
   ```

## Examples

### Basic Port Redirection
```bash
forward -p 8080:80
```
Redirects traffic from `http://localhost:80` to `http://localhost:8080`.

### Remote Server Tunneling
```bash
forward -s user@remote_server -p 8080:80
```
Redirects traffic from `remote_server:80` to `http://localhost:8080`.

### Docker Container Port Redirection
```bash
forward -d my_container -p 8080:80
```
Redirects traffic from the Docker container `my_container`'s port `80` to `http://localhost:8080`.

### Public Exposure
```bash
forward -p 8080:80 -P
```
Exposes `http://localhost:8080` publicly using localhost.run.

## Autocompletion

The script supports autocompletion for the following options:

- `-s` suggests SSH hosts from `~/.ssh/config` or `~/.ssh/known_hosts`.
- `-d` lists available Docker containers on the specified server or localhost.

To enable autocompletion, source the script:
```bash
source forward
```

## Termination

Use `Ctrl+C` to terminate the script and close all active tunnels.

## Requirements

- `ssh`
- `socat` (for local port redirection)
- Docker (if using the `-d` option)

