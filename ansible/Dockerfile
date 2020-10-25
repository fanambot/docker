# syntax=docker/dockerfile:experimental

FROM ubuntu:16.04
WORKDIR /root
ENV AWS_PROFILE="default"
COPY requirements.txt bashrc ./
RUN apt-get update && apt-get install -y build-essential libssl-dev libffi-dev python-dev ssh python curl vim sudo git \
    && curl -LO https://bootstrap.pypa.io/get-pip.py \
    && python get-pip.py \
    && rm get-pip.py \
    && pip install -r requirements.txt \
    && cat bashrc >> .bashrc \
    && rm -rf /var/cache/apt/* requirements.txt bashrc \
    && mkdir -p .ssh .aws /etc/ansible/inventory \
    && ssh-keyscan github.com >> .ssh/known_hosts \
    && echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config
COPY ec2.ini ec2.py /etc/ansible/inventory/
RUN chmod 700 /etc/ansible/inventory/ec2.py
RUN --mount=type=ssh,id=github git clone git@github.com:kalaibot/ansible.git
RUN ln -s /root/ansible/inventory/static /etc/ansible/inventory/static
EXPOSE 22
CMD ["/bin/bash"]
