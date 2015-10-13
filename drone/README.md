# Drone
This is a Docker image for the Drone CI system.

It is expected that you will copy the included `drone.toml.example` and set the source control credentials there before building.

## Build
To build your own image:

```bash
git clone https://github.com/arobson/docker-nonstop
cd docker-nonstop/drone
cp ./drone.toml.example ./drone.toml
nano ./drone.toml
docker build -t [yourDockerHubUserName]/drone .
```

## Use
The volume mounts shown in the example commands should point the container's docker and drone paths to your host box. I recommend this because it can take quite some time to sync your source control and get all the build images.

### Running a custom build
If you've built your own image from the `Dockerfile` and created your own `drone.toml`, use the following command to start your container:

```bash
   docker run --privileged \
				--name drone \
				-p [host]:80
				-v [hostpath]:/var/lib/docker
				-v [hostpath]:/var/lib/drone
				[yourDockerHubUserName]/drone
```

### Running my image
To use my image, use the following command to start the container with custom credentials (example shows github integration):

```bash
   docker run --privileged \
				--name drone \
				-p [host]:80
				-v [hostpath]:/var/lib/docker
				-v [hostpath]:/var/lib/drone
				-e DRONE_GITHUB_CLIENT="[your client application id]"
				-e DRONE_GITHUB_SECRET="[your client application secret]"
				arob/drone
```
