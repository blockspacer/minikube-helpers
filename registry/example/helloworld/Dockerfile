# Use the offical Golang image to create a build artifact.
# This is based on Debian and sets the GOPATH to /go.
# https://hub.docker.com/_/golang
FROM golang:1.12 as builder

# Copy local code to the container image.
WORKDIR /go/src/github.com/kameshsampath/minikube-helpers/registry/example/helloworld
COPY . .

# Build the command inside the container.
# (You may fetch or manage dependencies here,
# either manually or with a tool like "godep".)
RUN CGO_ENABLED=0 GOOS=linux go build -v -o helloworld

# Use a Docker multi-stage build to create a lean production image.
# https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds
FROM registry.fedoraproject.org/fedora-minimal

# Copy the binary to the production image from the builder stage.
COPY --from=builder /go/src/github.com/kameshsampath/minikube-helpers/registry/example/helloworld/helloworld /helloworld

CMD ["/helloworld"]