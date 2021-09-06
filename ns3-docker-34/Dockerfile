FROM ubuntu:18.04

LABEL Description="Docker image for NS-3 Network Simulator"

# NS-3
# Create working directory
RUN mkdir -p /usr/ns3
WORKDIR /usr

COPY . /usr

# Install needed packages
RUN set -x && \
    apt update && \
    apt install -y tzdata && \
    sh requirements.sh && \
    # Configure and compile NS-3
    cd /usr/ns-allinone-3.34/ns-3.34 && \
    ./waf configure --build-profile=debug --enable-examples --enable-tests && \
    ./waf && \
    # For visualizer
    cd /usr/ns-allinone-3.34/ && \
    wget https://files.pythonhosted.org/packages/7a/c6/14a9359621000ee5b7d5620af679be23f72c0ed17887b15228327427f97d/PyBindGen-0.22.0.tar.gz && \
    tar -xf PyBindGen-0.22.0.tar.gz && \
    # For click
    git clone https://github.com/kohler/click.git && \
    cd click && \
    ./configure --enable-userlevel --disable-linuxmodule --enable-nsclick && \
    make && \
    cd .. && \
    # For brite
    hg clone http://code.nsnam.org/BRITE && \
    cd BRITE && \
    make && \
    cd .. && \
    # For openflow
    hg clone http://code.nsnam.org/openflow && \
    cd openflow && \
    ./waf configure && \
    ./waf build && \
    # For integration
    cd /usr/ns-allinone-3.34/ns-3.34 && \
    ./waf configure --enable-examples --enable-tests --with-pybindgen=../PyBindGen-0.22.0 --with-nsclick=../click --with-brite=../BRITE --with-openflow=../openflow && \
    ./waf build && \
    # Make symlink
    ln -s /usr/ns-allinone-3.34/ns-3.34/ /usr/ns3/ && \
    # Cleanup
    apt clean && \
    rm -rf /var/lib/apt
