# Changelog

## v1.0.6

- Min k8s version 1.24
- Update fsgroup from 1000 to 33 (www-data)
- Added pvc for /var/www/html/custom directory (custom modules)

```yaml
# Custom modules persistence
custom:
  persistence:
    # -- Whether to create a pvc for the /var/www/html/custom directory.
    # @section -- Dolibarr deployment
    enabled: false
    # -- Labels of the documents pvc
    # @section -- Dolibarr deployment
    labels: { }
    # -- Annotations of the documents pvc
    # @section -- Dolibarr deployment
    annotations: { }
    # -- Size of the documents pvc
    # @section -- Dolibarr deployment
    size: 1Gi

```


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
