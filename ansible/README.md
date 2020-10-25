Run ansible in docker from local machine

To test the playbook against dev host, we can use this docker image from local machine

# Build image using this command - we use kalaibot ssh key to clone the ansible repository
DOCKER_BUILDKIT=1 docker build --ssh github=$HOME/.ssh/kalaibot -t ansible .

# Run the image
-v $HOME/.ssh/kalaibot:/root/.ssh/kalaibot -> mount kalaibot key to the container
-v $HOME/.aws/config:/root/.aws/config -> mount aws config to the container
-v $HOME/.aws/credentials:/root/.aws/credentials -> mount aws credentails to the container
-e AWS_PROFILE=primary-sa -> change the aws profile based on the host region

docker run --rm -it -v $HOME/.ssh/kalaibot:/root/.ssh/kalaibot \
-v $HOME/.aws/config:/root/.aws/config -v $HOME/.aws/credentials:/root/.aws/credentials -e AWS_PROFILE=primary-sa -w /root/juvo-ansible ansible
