# Docker Nonstop Service Host (Node)
This Docker image provides a runtime for any Node service built by Nonstop.

The value in this approach is that the container will be self-updating and pull down newer versions that match the package criteria set at start. This greatly reduces time between build and deployment to development environments.

## Building
Recommended naming convention is to tag your image with {node-version}-{nonstop-version}.

```bash
docker build -t yourAccount/nonstop-node:0.12.7-0.1.9 .
```

## Use
The Nonstop service host can be configured by environment variables.

This command template provides the minimal recommended set of environment variables for starting a new service container:

```bash
docker run --name [container name] \
	-e HOSTNAME=[container name] \
	-e SERVICE_NAME=core-juggerbaut \
	-e SERVICE_HOST_NAME=[host machine] \
	-e SERVICE_HOST_IP=10.209.64.104 \
	-e SERVICE_PORT_LOCAL=9090 \
	-e SERVICE_PORT_PUBLIC=8101 \
	-e INDEX_HOST=[index machine/address] \
	-e INDEX_PORT=[index port] \
	-e INDEX_TOKEN=[index token] \
	-e INDEX_FREQUENCY=60000 \
	-e PACKAGE_OWNER=[repository owner] \
	-e PACKAGE_PROJECT=[repository or project name] \
	-e PACKAGE_BRANCH=[repository branch] \
	-p [host port]:[service port] \
	arob/nonstop-node:0.12.7
```

### Environment Variables
| Group | Variable | Default |
|-------|-------------|---------|
| __Index__ | | |
| | INDEX_HOST | `"localhost"` |
| | INDEX_API | `"api"` |
| | INDEX_FREQUENCY | `300000` |
| | INDEX_PORT | `4444` |
| | INDEX_SSL | `false` |
| | INDEX_TOKEN | `""` |
| __Package__ | | |
| | PACKAGE_OWNER | `` |
| | PACKAGE_PROJECT | `` |
| | PACKAGE_BRANCH | `` |
| | PACKAGE_BUILD | `` |
| | PACKAGE_VERSION | `` |
| | PACKAGE__RELEASE_ONLY | `` |
| | PACKAGE_ARCHITECTURE | detected |
| | PACKAGE_PLATFORM | detected |
| | PACKAGE_FILES | `"./downloads"` |
| __Service__ | | |
| | SERVICE_NAME | `"service name"` |
| | SERVICE_HOST_NAME | `"service name"` |
| | SERVICE_HOST_IP | `"0.0.0.0"` |
| | SERVICE_PORT_LOCAL | `9090` |
| | SERVICE_PORT_PUBLIC | `9090` |

