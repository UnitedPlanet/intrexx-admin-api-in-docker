# Intrexx Admin API in Docker

__ATTENTION:__ Please refer to the Docker Hub page, for a list of available image names.

Run the Intrexx Admin API in Docker to manager your Intrexx portal via a REST API.

# Usage
A new instance of the Intrexx Admin API can be created as simply as follows:

```bash
docker run -e CACERTS_PATH=${PATH_TO_CACERTS_FILE} --name admin-api -d -p 4242:4242 unitedplanet/intrexx-admin-api:steady-latest
```
or (creating a self-signed certificate)
```bash
docker run -e CACERTS_SAN_LIST="dns:my.iaa.host ip:10.11.12.13" --name admin-api -d -p 4242:4242 unitedplanet/intrexx-admin-api:steady-latest
```

Providing a keystore, containing a valid certificate for the host is mandatory. Aside from that, some configuration parameters are expected to be provided via environment vars.

## Custom configuration work
It is possible for the user to provide additional initialization scripts, placed under `/entrypoint.d/`. Any `*.sh` script found there, will be executed by the `docker-entrypoint.sh` routine. Please do not replace the entire directory as needed initialization scripts are already stored there in the original image provided by United Planet. Instead use a Dockerfile and the COPY command, to store your scripts in the directory.

# Tags

The Intrexx Admin API images are tagged with the semantic version of the Intrexx releases. The semantic version contains 3 parts:

- Major version
- Minor version
- Patch level

Additionally for every major version, there is a specific latest tag, e.g. `steady-latest`. This may be used to automatically receive the most recent patches but to avoid major version upgrades.

Please refer to the [Docker Hub page](https://hub.docker.com/r/unitedplanet/intrexx-admin-api) for a complete list of available tags.

# List of environment vars
Name | Default value | Description
--- | --- | ---
`PORTAL_NAME` | portal | The name of the portal to administer.
`PORTAL_HOST` | portal | The DNS of the portal host.
`PORTAL_API_PORT` | 8101 | The public port of the portal's REST API.
`PORTAL_API_SCHEME` | https | Connection scheme the Admin API uses to connect to the portal.
`PORTAL_ADMIN_USER` | Administrator | The portal's admin user name.
`PORTAL_ADMIN_PW` | NONE | The password of the portal's admin user. Use `NONE` for an empty password.
`IAA_USER` | iaa-admin | Administrator user of the Intrexx Admin API.
`IAA_PW` | P4$$w0rD | Password of the Administrator user of the Intrexx Admin API.
`IAA_DEBUG_MODE` | false | Set this to true, to enable debug mode of the Intrexx Admin API.
`CACERTS_PATH` | UNDEFINED | Path of the keystore containing the Admin API Hosts certificate (within the container).
`CACERTS_PW` | changeit | Password for the keystore containing the Admin API Hosts certificate.
`CACERTS_SAN_LIST` |  | Parameter list for creating a self-signed certificate. Elements must begin with ip: or dns: .
`IAA_SECRET` | changeit | Secret used to encode the JWTs.
`IAA_USE_SSL` | true | Boolean Parameter to optionally disable SSL.
`IAA_LICENSE` | NONE | License key for IAA, needed in version 11.0.0 and newer.
