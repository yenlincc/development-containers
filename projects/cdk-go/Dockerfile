# The following image should've already been built by GitHub Action
# in an earlier step before attempting to build this Dockerfile
FROM thinkthenrant/development-container-go:for-auto-build

RUN sudo apt-get update \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
    # needed by the nodejs installer
    gnupg \
    # need to unzip aws cli v2
    unzip \
    # less is needed by aws cli v2
    less \
    && sudo DEBIAN_FRONTEND=noninteractive curl -sL https://deb.nodesource.com/setup_14.x  | sudo DEBIAN_FRONTEND=noninteractive bash - \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends nodejs \
    && node -v && npm -v \
    && sudo npm install -g aws-cdk aws-cdk-local \
    && sudo curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && sudo unzip awscliv2.zip \
    && sudo ./aws/install \
    && sudo rm -r awscliv2.zip ./aws \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get purge -y unzip \
    && aws --version && cdk --version
