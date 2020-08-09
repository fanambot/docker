FROM ubuntu:18.04

MAINTAINER kalaiucd@gmail.com

RUN apt update && apt install -y telnet && \
    rm -rf /var/cache/apt/*

ENTRYPOINT ["sh","-c","sleep infinity"]
