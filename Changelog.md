# Changelog

## v1.0.5

- Fixed secrets values section. Previously, 'generate' value was taken from the db secret section.
  
```yaml
secrets:
  # -- Dolibarr admin password secret. When true, no secret is provisioned.
  # @section -- Dolibarr deployment
  skip: false
  # -- Whether to generate the dolibarr admin password on secret creation.
  # @section -- Dolibarr deployment
  generate: true
  # -- When generate is false, the admin password to put in the secret. Overwrites existing values
  # @section -- Dolibarr deployment
  adminPassword: ''
```


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
