## DEFINE BASE IMAGE FOR MINIMAL IMAGE
FROM registry.access.redhat.com/ubi8/ubi-minimal:8.4

## CREATE OPENSCAP WORKING DIRECTORY
WORKDIR /OpenSCAP

## COPY CUSTOM REPOS
COPY custom.repo /etc/yum.repos.d/custom.repo

## UPDATE IMAGE REPOS & UPDATE ENTRYPOINT
RUN chmod 644 /etc/yum.repos.d/custom.repo && \
    rm -f /etc/yum.repos.d/ubi.repo && \
    microdnf repolist && \
    microdnf update -y

## DOWNLOAD OSCAP-PODMAN TOOL & DEPENDS, INSTALL AND CLEANUP
RUN curl -L https://rpmfind.net/linux/centos/8-stream/AppStream/x86_64/os/Packages/openscap-utils-1.3.5-2.el8.x86_64.rpm -o openscap-utils-1.3.5-2.el8.x86_64.rpm && \
    curl -L https://rpmfind.net/linux/centos/8-stream/AppStream/x86_64/os/Packages/openscap-1.3.5-2.el8.x86_64.rpm -o openscap-1.3.5-2.el8.x86_64.rpm && \
    curl -L https://rpmfind.net/linux/centos/8-stream/AppStream/x86_64/os/Packages/openscap-scanner-1.3.5-2.el8.x86_64.rpm -o openscap-scanner-1.3.5-2.el8.x86_64.rpm && \
    curl -L https://rpmfind.net/linux/centos/8-stream/AppStream/ppc64le/os/Packages/rpmdevtools-8.10-8.el8.noarch.rpm -o rpmdevtools-8.10-8.el8.noarch.rpm && \
    microdnf install dnf unzip podman -y && \
    dnf install rpmdevtools-8.10-8.el8.noarch.rpm openscap-scanner-1.3.5-2.el8.x86_64.rpm openscap-1.3.5-2.el8.x86_64.rpm openscap-utils-1.3.5-2.el8.x86_64.rpm -y && \
    dnf clean all && \
    rm -rf /var/cache/dnf/ /var/tmp/* /tmp/* /var/tmp/.???* /tmp/.???* openscap-utils-1.3.5-2.el8.x86_64.rpm openscap-1.3.5-2.el8.x86_64.rpm openscap-scanner-1.3.5-2.el8.x86_64.rpm rpmdevtools-8.10-8.el8.noarch.rpm

## DEFINE ENTRYPOINT SCRIPT
ENTRYPOINT ["/bin/bash"]