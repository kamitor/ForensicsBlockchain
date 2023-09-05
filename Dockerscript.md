``` # Use the official Ubuntu as the base image
FROM ubuntu:latest

# Set environment variables to avoid interactive prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

# Install required packages
RUN apt-get update && apt-get install -y \
    git \
    wget \
    curl \
    build-essential

# Install BlockSci
RUN git clone https://github.com/citp/BlockSci.git /opt/BlockSci && \
    cd /opt/BlockSci && \
    ./install.sh

# Install Ethereum tools (Geth and Truffle)
RUN apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:ethereum/ethereum && \
    apt-get update && \
    apt-get install -y ethereum && \
    apt-get install -y nodejs && \
    apt-get install -y npm && \
    npm install -g ethereumjs-testrpc truffle

# Install Truffle
RUN npm install -g truffle

# Install Etherscan Dapp
RUN git clone https://github.com/etherscan/dapp.git /opt/etherscan-dapp

# Install Nansen (Note: Nansen may not be available as open-source)
# This section assumes that you have a method to install Nansen or have obtained the necessary files for installation.

# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set the working directory
WORKDIR /opt

# Expose ports if needed
# EXPOSE 8545

# Start a shell when the container runs
CMD ["/bin/bash"]
```

```
```bash
docker build -t blockchain-tools .

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcwMDM2NjU4XX0=
-->