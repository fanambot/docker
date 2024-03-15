FROM ubuntu:18.04

LABEL description="This image has all neccessary packages to debug"

MAINTAINER kalaiucd@gmail.com

RUN apt update && apt install -y curl telnet dnsutils iputils-ping nmap hey apache2-utils && \
    rm -rf /var/cache/apt/*

ENTRYPOINT ["sh","-c","sleep infinity"]
