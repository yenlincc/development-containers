FROM thinkthenrant/development-container-go:dev

# https://rustc-dev-guide.rust-lang.org/building/prerequisites.html
RUN sudo apt-get update \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
    # needed by the nodejs installer
    gnupg \
    && curl -sL https://deb.nodesource.com/setup_14.x  | bash - \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends nodejs \
    && node -v && npm -v \
    && npm install -g aws-cdk \
    && cdk --version
