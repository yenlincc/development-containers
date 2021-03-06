FROM thinkthenrant/development-container-go:dev

# https://rustc-dev-guide.rust-lang.org/building/prerequisites.html
RUN sudo apt-get update \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
    # needed by the nodejs installer
    gnupg \
    && sudo DEBIAN_FRONTEND=noninteractive curl -sL https://deb.nodesource.com/setup_14.x  | sudo DEBIAN_FRONTEND=noninteractive bash - \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends nodejs \
    && node -v && npm -v \
    && sudo npm install -g aws-cdk \
    && cdk --version