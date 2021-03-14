FROM thinkthenrant/development-container-go:dev

# https://rustc-dev-guide.rust-lang.org/building/prerequisites.html
RUN sudo apt-get update \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
    # needed by the nodejs installer
    gnupg unzip \
    && sudo DEBIAN_FRONTEND=noninteractive curl -sL https://deb.nodesource.com/setup_14.x  | sudo DEBIAN_FRONTEND=noninteractive bash - \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends nodejs \
    && node -v && npm -v \
    && sudo npm install -g aws-cdk aws-cdk-local \
    && sudo curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && sudo unzip awscliv2.zip \
    && sudo ./aws/install \
    && sudo rm -r awscliv2.zip ./aws \
    && aws --version && cdk --version
