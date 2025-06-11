FROM registry.access.redhat.com/ubi9/ubi-minimal:latest

WORKDIR /

RUN microdnf install -y git gcc-c++ libcurl-devel libedit-devel libuuid-devel libxml2-devel ncurses-devel python3-devel rsync sqlite-devel unzip zip tar && \
    microdnf clean all

ENV SWIFTLY_BIN_DIR="/swift/usr/bin"

RUN echo "Downloading Swiftly" && \
    curl -O https://download.swift.org/swiftly/linux/swiftly-$(uname -m).tar.gz && \
    tar zxf swiftly-$(uname -m).tar.gz && \
    rm -fr swiftly-$(uname -m).tar.gz && \
    chmod -R o+x swiftly && \
    ./swiftly init --quiet-shell-followup && \
    $SWIFTLY_BIN_DIR/swiftly install --use 6.1.2 && \
    $SWIFTLY_BIN_DIR/swift --version && \
    $SWIFTLY_BIN_DIR/swift sdk install https://download.swift.org/swift-6.1.2-release/static-sdk/swift-6.1.2-RELEASE/swift-6.1.2-RELEASE_static-linux-0.0.1.artifactbundle.tar.gz --checksum df0b40b9b582598e7e3d70c82ab503fd6fbfdff71fd17e7f1ab37115a0665b3b && \
    $SWIFTLY_BIN_DIR/swift sdk list

