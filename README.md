# ej-shafran/container-action

## Usage

```yml
on:
  - push
  - pull_request

jobs:
  test:
    - uses: actions/checkout@v4
    - uses: ej-shafran/container-action@v1
      with:
        name: "test-db"
        image: "mysql:latest"
        docker-options: "-p 3306:3306 -e MYSQL_DATABASE=test-db MYSQL_ROOT_PASSWORD=test"
    # Some code that uses the database...
    # The container will be cleaned up in the post-action
```

## Inputs

### `name`

**Required** (_type:_ `string`) The name for the container.

### `image`

**Required** (_type:_ `string`) The image to run for the container. Is passed directly to `docker run` and so it can include the tag of the image. The image will be run with [the `-d` flag](https://docs.docker.com/reference/cli/docker/container/run/#detach) and [the `--rm` flag](https://docs.docker.com/reference/cli/docker/container/run/#rm).

### `docker-options`

**Optional** (_type:_ `string`) Additional CLI options to pass to `docker run`. Can be used to setup port mapping, environment variables, restart policy, etc.
