To install PhoneInfoga, you'll need to download the binary or build the software from source code.

## Download binary

Follow the instructions :

- Go to [release page on GitHub]()
- Choose your OS and architecture
- Download the archive, extract the binary then run it in a terminal

```shell
# Download the archive
# !! Replace <version> by the latest version
curl -sSL "https://github.com/sundowndev/phoneinfoga/releases/download/<version>/phoneinfoga_$(uname -s)_$(uname -m).tar.gz" -o ./phoneinfoga.tar.gz

# Extract the binary
tar xfv phoneinfoga.tar.gz

# Run the software
./PhoneInfoga --help

# Install it globally
mv ./PhoneInfoga /usr/bin/phoneinfoga
```

## Install globally with Go

```shell
go get -u github.com/sundowndev/PhoneInfoga
```

## Build from source

Follow the instructions :

```shell
# Clone the repository
git clone https://github.com/sundowndev/PhoneInfoga
cd PhoneInfoga/

# Install requirements
go get -v -t -d ./...

# Install packr2
go get -u github.com/gobuffalo/packr/v2/packr2

# Build web client assets
(cd client && yarn && yarn build)

# You need Packr v2 to inject assets inside the binary
packr2 build -o phoneinfoga

packr2 clean

./phoneinfoga
```

## Using Docker

### From docker hub

You can pull the repository directly from Docker hub

```shell
docker pull sundowndev/phoneinfoga:latest
```

Then run the tool

```shell
docker run --rm -it sundowndev/phoneinfoga version
```

### Docker-compose

You can use a single docker-compose file to run the tool without downloading the source code.

```
version: '3.7'

services:
    phoneinfoga:
      container_name: phoneinfoga
      restart: on-failure
      build:
        context: .
        dockerfile: Dockerfile
      command:
        - "serve"
      ports:
        - "80:5000"
```

### From the source code

You can download the source code, then build the docker images

#### Build

This will automatically pull, build then setup services (such as web client and REST API)

```shell
docker-compose up -d
```

#### CLI usage

```shell
docker-compose run --rm phoneinfoga --help
```

#### Troubleshooting

All output is sent to stdout so it can be inspected by running:

```shell
docker logs -f <container-id|container-name>
```
