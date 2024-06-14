FROM registry.access.redhat.com/ubi9/ubi-minimal:latest

WORKDIR /

RUN microdnf install -y git gcc-c++ libcurl-devel libedit-devel libuuid-devel libxml2-devel ncurses-devel python3-devel rsync sqlite-devel unzip zip tar && \
    microdnf clean all

RUN export today=$(date '+%Y-%m-%d') && \
    export yesterday=$(date --date="${today} -1 day" '+%Y-%m-%d') && \
    curl -o swift.tar.gz "https://download.swift.org/swift-6.0-branch/ubi9/swift-6.0-DEVELOPMENT-SNAPSHOT-${yesterday}-a/swift-6.0-DEVELOPMENT-SNAPSHOT-${yesterday}-a-ubi9.tar.gz" && \
    tar zxf swift.tar.gz && \
    rm -fr swift.tar.gz && \
    mv swift* swift && \
    chmod -R o+x /swift/usr/bin/ && \
    cd /swift/usr/bin/ && \
    swift sdk install https://download.swift.org/swift-6.0-branch/static-sdk/swift-6.0-DEVELOPMENT-SNAPSHOT-2024-06-08-a/swift-6.0-DEVELOPMENT-SNAPSHOT-2024-06-08-a_static-linux-0.0.1.artifactbundle.tar.gz && \
    swift sdk list

