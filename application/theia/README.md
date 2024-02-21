# Eclipse Theia: Cloud-Based IDE for Development

## Dockerfile

This Dockerfile utilizes a Node.js image as its base and installs necessary supported packages along with Python.

## Docker Build


## Docker Build:
```bash 
docker build . -t balumaduru/theia-for-development:0.0.1
```

## Running Theia
To run Theia, execute the following command:
```bash
docker run -it --init -p 3000:3000 -v "$(pwd):/home/project" balumaduru/theia-for-development:0.0.1
```