# grpc-web-example

This repository demonstrates the usage of grpc-web with vuejs and a Go microservice.

## Directories:
* api - Contains the gRPC/proto definitions
* envoy - Contains the envoy configuration for grpc-web to grpc proxying
* time - time microservice in Go, listens on port 9090 for gRPC connections
* frontend - simple vuejs application

## Usage:
* `make proto` - Generate proto clients
* `make run-frontend` - Start frontend
* `make run-servers` - Start Time services and Envoy proxy

## Linux
docker run -v `pwd`/api:/api -v `pwd`/time/goclient:/goclient -v `pwd`/frontend/src/jsclient:/jsclient jfbrandhorst/grpc-web-generators protoc -I /api --go_out=plugins=grpc,paths=source_relative:/goclient --js_out=import_style=commonjs:/jsclient --grpc-web_out=import_style=commonjs,mode=grpcwebtext:/jsclient /api/time/v1/time_service.proto

## Windows
docker run -v "%cd%"/api:/api -v "%cd%"/time/goclient:/goclient -v "%cd%"/frontend/src/jsclient:/jsclient jfbrandhorst/grpc-web-generators protoc -I /api --go_out=plugins=grpc,paths=source_relative:/goclient --js_out=import_style=commonjs:/jsclient --grpc-web_out=import_style=commonjs,mode=grpcwebtext:/jsclient /api/time/v1/time_service.proto