FROM thinkthenrant/development-container-rust:dev

# https://rustc-dev-guide.rust-lang.org/building/prerequisites.html
RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    build-essential openssl libssl-dev pkg-config liblz4-tool \
    # install Docker
    && apt-get install -y apt-transport-https \
    gnupg-agent software-properties-common \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) \
        stable" \
    && apt-get update && apt-get install -y docker-ce docker-ce-cli containerd.io
RUN ${HOME}/.cargo/bin/cargo install cargo-make \
    && ${HOME}/.cargo/bin/cargo install cargo-deny --version 0.8.5