FROM registry.access.redhat.com/ubi9/ubi-minimal:latest

WORKDIR /

RUN microdnf install -y git gcc-c++ libcurl-devel libedit-devel libuuid-devel libxml2-devel ncurses-devel python3-devel rsync sqlite-devel unzip zip tar && \
    microdnf clean all

RUN export today=$(date '+%Y-%m-%d') && \
    export day_before=1 && \
    export day_of_week=$(date '+%w') && \
    if (( day_of_week < 2 )) || (( day_of_week > 5 )); then export day_before=4; fi && \
    if ((day_of_week == 5 )); then export day_before=2; fi && \
    export last_nightly=$(date --date="${today} -${day_before} day" '+%Y-%m-%d') && \
    echo "Downloading Swift development snapshot from ${last_nightly}" && \
    curl -o swift.tar.gz "https://download.swift.org/swift-6.0-branch/ubi9/swift-6.0-DEVELOPMENT-SNAPSHOT-${last_nightly}-a/swift-6.0-DEVELOPMENT-SNAPSHOT-${last_nightly}-a-ubi9.tar.gz" && \
    tar zxf swift.tar.gz && \
    rm -fr swift.tar.gz && \
    mv swift* swift && \
    chmod -R o+x /swift/usr/bin/ && \
    /swift/usr/bin/swift sdk install https://download.swift.org/swift-6.0-branch/static-sdk/swift-6.0-DEVELOPMENT-SNAPSHOT-2024-06-22-a/swift-6.0-DEVELOPMENT-SNAPSHOT-2024-06-22-a_static-linux-0.0.1.artifactbundle.tar.gz && \
    /swift/usr/bin/swift sdk list

