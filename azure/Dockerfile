FROM ubuntu:18.04
RUN apt-get update && apt-get install wget unzip software-properties-common build-essential \
   zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev python3-distutils python3-apt -y \
   && wget https://releases.hashicorp.com/terraform/0.14.11/terraform_0.14.11_linux_amd64.zip \
   && unzip terraform_0.14.11_linux_amd64.zip \
   && mv terraform /usr/local/bin/ \
   && wget https://bootstrap.pypa.io/get-pip.py 
COPY requirements.txt /
RUN add-apt-repository ppa:deadsnakes/ppa -y \
   && apt update \
   && apt install python3.8 -y \
   && python3.8 get-pip.py \
   && pip install -r requirements.txt \
   && rm -rf terraform_0.14.11_linux_amd64.zip get-pip.py
