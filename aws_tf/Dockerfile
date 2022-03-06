FROM amazon/aws-cli
RUN curl -O https://releases.hashicorp.com/terraform/0.14.11/terraform_0.14.11_linux_amd64.zip \
   && yum update \
   && yum install unzip -y \
   && unzip terraform_0.14.11_linux_amd64.zip \
   && mv terraform /usr/local/bin/ \
   && mkdir /root/.aws \
   && rm -rf terraform_0.14.11_linux_amd64.zip
ENTRYPOINT ["/bin/sh"]
