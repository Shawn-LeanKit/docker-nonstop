# Nonstop index
A Docker container for running the nonstop index that service hosts crave.

## Setup
You'll need to start the container in shell mode so that you can run `nsindex` and set credentials the first time.

```bash
sudo docker run -it \
	-v [host volume]:/home/ubuntu/data \
	-v [host volume]:/home/ubuntu/public \
	--name nonstop-index
	--restart=always
	arob/nonstop-index
	bash
```

To run the setup:
```bash
~/setup.sh
```

Use the console menu to generate credentials or edit the .db files ( `users` ) to change credentials and/or add tokens. Exit the container.

## Starting The Container
Once you have set everything up in the container, you'll want to run it as a daemon:

```bash
sudo docker run -d \
	-v [host volume]:/home/ubuntu/data \
	-v [host volume]:/home/ubuntu/public \
	-e HOSTNAME=nonstop-index \
	-p 4444:4444 \
	--restart=always
	nonstop-index
```

## Running A Newer Version
The index can be run from a fresh image without setup as long as you keep the mapped volumes remain in the same location (the data one being most important):

```bash
sudo docker run -d \
	-v [host volume]:/home/ubuntu/data \
	-v [host volume]:/home/ubuntu/public \
	-e HOSTNAME=nonstop-index \
	-p 4444:4444 \
	--name nonstop-index \
	--restart=always
	arob/nonstop-index
```

recommended bash script:
```bash
docker pull arob/nonstop-index
docker rm -f nonstop-index
docker run -d --name nonstop-index --restart=always -v ~/nsdata:/home/ubuntu/data -v ~/packages:/home/ubuntu/public -e HOSTNAME=nonstop-index -p 4444:4444 arob/nonstop-index
```

## Updating nonstop-index version
Change the version in the Dockerfile, build and push to the registry.
