## Use small, minimal base images
Use Alpine or slim variants.
Smaller images = faster pulls, less attack surface.

## Always pin verion, never use latest
FROM node:22-alpine

## Keep Dockerfile simple & multi-stage builds
***Example:*** Bricks, if bottom layer is changed everything gets changes.
FROM golang:1.22 as builder
WORKDIR /app
COPY . .
RUN go build -o myapp

FROM alpine:3
COPY --from=builder /app/myapp .
CMD ["./myapp"]

*** This produces tiny final image ***
Having multiple docker files, one file used as builder, we copy content required from that to final image.
This process can remove un-neccessary installations, build cache & etc.
We only copy compiled to code, no dependencies needed for compiling.


## Use .dockerignore
Avoid copying unnecessary files.

## Do not run containers as root
RUN addgroup --system app && adduser --system --ingroup app app
USER app

## Set explicit WORKDIR
WORKDIR /app

## Don’t install unnecessary tools
No curl, vim, gcc unless needed.
Your image should NOT be a VM.

## Keep layers small
Each RUN creates a layer. Combine commands:
RUN apk update && apk add --no-cache curl

## Use ENTRYPOINT + CMD properly
ENTRYPOINT = fixed command
CMD = arguments
ENTRYPOINT ["python"]
CMD ["app.py"]

## Use environment variables for config
ENV PORT=8080

## Don’t store secrets in images
Use:
 kubernetes secrets
 AWS secret manager
 Vault

## Make containers stateless
No writing inside the container filesystem.
Use:
Volumes
S3
Databases

## Expose correct ports
EXPOSE 8080

## Prefer COPY over ADD
COPY is predictable.
ADD does extra things (like unpack tar) that you may not want.

## Don’t install extra OS packages
Each package increases vulnerability risk.

## Scan images regularly
docker scan
Trivy(best)

## Tag images well
myapp:1.2.1
myapp:2025-11-25
myapp:prod

## Keep containers small & fast
target <100MB

## Log to stdout / stderr
Never write logs to files.
Docker/Kubernetes expect logs via stdout.
