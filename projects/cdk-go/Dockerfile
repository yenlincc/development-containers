# The following image should've already been built by GitHub Action
# in an earlier step before attempting to build this Dockerfile
FROM ghcr.io/yenlincc/development-container-go:for-auto-build

# Ref: https://docs.docker.com/engine/reference/builder/#automatic-platform-args-in-the-global-scope
ARG TARGETOS
ARG TARGETARCH
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
    && sudo npm install -g aws-cdk-lib aws-cdk-local \
    if [ "${TARGETARCH}" = 'amd64' ]; then \
        CLI_ARCH='x86_64' \
    elif [ "${TARGETARCH}" = 'arm64' ] \
        CLI_ARCH='aarch64' \
    fi \
    && sudo curl "https://awscli.amazonaws.com/awscli-exe-${TARGETOS}-${CLI_ARCH}.zip" -o "awscliv2.zip" \
    && sudo unzip awscliv2.zip \
    && sudo ./aws/install \
    && sudo rm -r awscliv2.zip ./aws \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get purge -y unzip \
    && aws --version && cdk --version
