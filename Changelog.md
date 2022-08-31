# Changelog

## v1.0.3

- Added db deployment configuration options:

```yaml
db:

  deployment:
    imageName: mariadb
    imageTag: 10.6.5

  resources:
    request:
      memory: '256Mi'
      cpu: '50m'

  env: { }

```
