# docker_compose

Automates installation, configuration, and state management of Docker Compose services

## Table of contents

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [docker_compose_actions](#docker_compose_actions)
  - [docker_compose_buildx_version](#docker_compose_buildx_version)
  - [docker_compose_config](#docker_compose_config)
  - [docker_compose_containerd_version](#docker_compose_containerd_version)
  - [docker_compose_dest_dir](#docker_compose_dest_dir)
  - [docker_compose_docker_version](#docker_compose_docker_version)
  - [docker_compose_file_group](#docker_compose_file_group)
  - [docker_compose_file_owner](#docker_compose_file_owner)
  - [docker_compose_recreate](#docker_compose_recreate)
  - [docker_compose_secret_env](#docker_compose_secret_env)
  - [docker_compose_state_action](#docker_compose_state_action)
  - [docker_compose_version](#docker_compose_version)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.20`

## Default Variables

### docker_compose_actions

List of actions the role does, accepts one or more actions.
Use comma without spaces as a delimiter for multiple actions.

**_Required:_** `true`<br />
**_Type:_** String<br />

#### Example usage

```YAML
  docker_compose_actions: install
  docker_compose_actions: install,upload_config
```

### docker_compose_buildx_version

docker-buildx-plugin package version for installation

**_Required:_** `true`, only in case `docker_compose_actions: install`<br />
**_Type:_** String<br />

#### Default value

```YAML
docker_compose_buildx_version: 0.24.0-1~ubuntu.24.04~noble
```

### docker_compose_config

Content of the docker-compose.yml file to upload

**_Required:_** `true`, only in case `docker_compose_actions: upload_config`<br />
**_Type:_** String<br />

#### Example usage

```YAML
docker_compose_config:
  services:
    app:
      image: myapp:latest
      ports:
        - 8080:8080
```

### docker_compose_containerd_version

containerd.io package version for installation

**_Required:_** `true`, only in case `docker_compose_actions: install`<br />
**_Type:_** String<br />

#### Default value

```YAML
docker_compose_containerd_version: 1.7.27-1
```

### docker_compose_dest_dir

Directory where docker-compose.yml will be uploaded

**_Required:_** `true`, only in case `docker_compose_actions: upload_config`<br />
**_Type:_** String<br />

#### Default value

```YAML
docker_compose_dest_dir: /opt/docker_compose
```

### docker_compose_docker_version

docker-ce and docker-ce-cli package version for installation

**_Required:_** `true`, only in case `docker_compose_actions: install`<br />
**_Type:_** String<br />

#### Default value

```YAML
docker_compose_docker_version: 5:28.2.2-1~ubuntu.24.04~noble
```

### docker_compose_file_group

Group of the uploaded docker-compose.yml file

**_Type:_** String<br />

#### Default value

```YAML
docker_compose_file_group: root
```

### docker_compose_file_owner

Owner of the uploaded docker-compose.yml file

**_Type:_** String<br />

#### Default value

```YAML
docker_compose_file_owner: root
```

### docker_compose_recreate

Controls whether `docker compose up` recreates containers (only in case
`docker_compose_actions: state_control`). `auto` (the module default)
only recreates containers whose resolved configuration actually changed;
`always` forces recreation of every container regardless of detected
drift; `never` leaves existing containers untouched even if config
differs.

**_Required:_** `false`<br />
**_Type:_** String<br />

#### Default value

```YAML
docker_compose_recreate: auto
```

#### Example usage

```YAML
  docker_compose_recreate: always
```

### docker_compose_secret_env

Dict of environment variables passed to the `docker compose` process
invocation only (only in case `docker_compose_actions: state_control`) -
never written to disk. Use this for secrets that the uploaded
docker-compose.yml references via `${VAR}` interpolation (e.g.
`SECRET_KEY: ${SECRET_KEY}`), instead of baking literal values into
docker_compose_config or writing a `.env` file under
docker_compose_dest_dir. Note this only keeps secrets out of the
uploaded compose file and any `.env` file - Docker itself still persists
each container's fully-resolved environment to
/var/lib/docker/containers/<id>/config.v2.json regardless of injection
method, so this does not remove root/docker-group access to secrets on
the host, only reduces the number of on-disk copies. When non-empty, the
state_control task result is suppressed (no_log) to keep these values out
of Ansible's own logs.

**_Required:_** `false`<br />
**_Type:_** Dict<br />

#### Default value

```YAML
docker_compose_secret_env: {}
```

#### Example usage

```YAML
docker_compose_secret_env:
  SECRET_KEY: '{{ plane_secret_key }}'
  POSTGRES_PASSWORD: '{{ plane_db_password }}'
```

### docker_compose_state_action

Controls state of Docker Compose services

**_Required:_** `true`, only in case `docker_compose_actions: state_control`<br />
**_Type:_** String<br />

#### Example usage

```YAML
  docker_compose_state_action: present
  docker_compose_state_action: stopped
  docker_compose_state_action: absent
  docker_compose_state_action: restarted
```

### docker_compose_version

docker-compose-plugin package version for installation

**_Required:_** `true`, only in case `docker_compose_actions: install`<br />
**_Type:_** String<br />

#### Default value

```YAML
docker_compose_version: 2.36.2-1~ubuntu.24.04~noble
```

## Dependencies

None.

## License

MIT

## Author

freedform
