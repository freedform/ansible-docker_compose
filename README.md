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
          - "8080:8080"
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
