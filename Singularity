Bootstrap: docker
From: ubuntu:16.04

%labels
Maintainer Matthew Flister
Version v1.0

%help
# Add information describing your container.
This container includes Python.

%environment
    # Set useful environment variables here. This section is used only at runtime, not during build.
    export PATH=/opt/python/bin:$PATH
    export LD_LIBRARY_PATH=/opt/python/lib:$LD_LIBRARY_PATH

%post
    # Add build commands here. These commands are only run at build time.

    # Create useful bind points for needed file systems. The following are set by default in RCC and should always be included for containers used in RCC.
    mkdir -p /scratch/global /scratch/local /rcc/stor1/refdata /rcc/stor1/projects /rcc/stor1/depts

    # Install necessary packages.
    apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        gcc-multilib \
        ca-certificates \
        zlib1g-dev \
        libssl-dev \
        curl
    apt-get clean
    rm -rf /var/lib/apt/lists/*

    # Install Python from source.
    export PATH=/opt/python/bin:$PATH
    curl https://www.python.org/ftp/python/2.7.15/Python-2.7.15.tgz -o Python-2.7.15.tgz
    tar -xvf Python-2.7.15.tgz && cd Python-2.7.15
    ./configure --prefix=/opt/python && make && make install
    rm -rf Python-2.7.15*

    # Install pip package manager.
    curl https://bootstrap.pypa.io/get-pip.py | python

    # Install some useful Python packages.
    pip install --upgrade numpy scipy matplotlib 

%test
    /opt/python/bin/python --version
