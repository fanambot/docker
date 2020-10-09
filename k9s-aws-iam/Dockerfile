# -----------------------------------------------------------------------------
# The base image for building the k9s binary
# docker run --rm -it -v ~/.kube/config:/root/.kube/config -v ~/.aws/credentials:/root/.aws/credentials <docker image name>

FROM golang:1.15.2-alpine3.12 AS build
WORKDIR /k9s
COPY go.mod go.sum main.go Makefile ./
COPY internal internal
COPY cmd cmd
RUN apk --no-cache add make git gcc libc-dev curl && make build

# -----------------------------------------------------------------------------
# Build the final Docker image

FROM alpine:3.12.0
ARG KUBECTL_VERSION="v1.18.6"
ARG AWS_IAM_AUTH_VERSION_URL=https://amazon-eks.s3.us-west-2.amazonaws.com/1.17.9/2020-08-04/bin/linux/amd64/aws-iam-authenticator
COPY --from=build /k9s/execs/k9s /bin/k9s
RUN mkdir /root/.aws
RUN apk add --update ca-certificates \
  && apk add --update -t deps curl vim python3 py3-pip \
  && pip3 install --upgrade pip \
  && pip3 install awscli \
  && curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
  && chmod +x /usr/local/bin/kubectl \
  && curl -LO ${AWS_IAM_AUTH_VERSION_URL} \
  && mv aws-iam-authenticator /usr/local/bin/aws-iam-authenticator \
  && chmod +x /usr/local/bin/aws-iam-authenticator \
  && apk del --purge deps \
  && rm /var/cache/apk/*
ENTRYPOINT [ "/bin/k9s" ]