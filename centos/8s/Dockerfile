FROM quay.io/centos/centos:stream8
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"

# Singularity build system
RUN sed -i s/mirror.centos.org/vault.centos.org/g /etc/yum.repos.d/*.repo && \
    sed -i s/^#.*baseurl=http/baseurl=http/g /etc/yum.repos.d/*.repo && \
    sed -i s/^mirrorlist=http/#mirrorlist=http/g /etc/yum.repos.d/*.repo
RUN dnf -y install epel-release
RUN dnf groupinstall -y 'Development Tools'
RUN dnf install -y openssl-devel libuuid-devel wget squashfs-tools golang which python36 cryptsetup
RUN dnf -y install openssh-clients e2fsprogs fakeroot fuse-overlayfs squashfuse fuse3-devel
#
# Final update and creation of the package list
RUN dnf -y update && \
    echo "el8" > /build-platform && \
    rpm -qa > /var/lib/package-list
COPY build-singularity build-apptainer /bin/
