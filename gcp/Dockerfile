FROM google/cloud-sdk

RUN mkdir /automation && apt update && apt install -y zip

WORKDIR /automation

RUN curl -O https://releases.hashicorp.com/terraform/1.4.2/terraform_1.4.2_linux_amd64.zip

RUN unzip terraform_1.4.2_linux_amd64.zip

RUN mv terraform /usr/local/bin
