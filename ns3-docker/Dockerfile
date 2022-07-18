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
    apt install -y tzdata gdb&& \
    sh requirements.sh && \
    # Configure and compile NS-3
    cd /usr/ns-allinone-3.35/ns-3.35 && \
    ./waf configure --build-profile=debug --enable-examples --enable-tests && \
    ./waf && \
    # For visualizer
    cd /usr/ns-allinone-3.35/ && \
    wget https://github.com/gjcarneiro/pybindgen/archive/refs/tags/0.22.1.tar.gz && \
    tar -xf 0.22.1.tar.gz && \
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
    cd /usr/ns-allinone-3.35/ns-3.35 && \
    ./waf configure --build-profile=debug --enable-examples --enable-tests --with-pybindgen=../PyBindGen-0.22.1 --with-nsclick=../click --with-brite=../BRITE --with-openflow=../openflow && \
    ./waf build && \
    # Make symlink
    ln -s /usr/ns-allinone-3.35/ns-3.35/ /usr/ns3/ && \
    # Cleanup
    apt clean && \
    rm -rf /var/lib/apt
