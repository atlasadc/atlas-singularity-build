FROM centos:7
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"

# Singularity build system
COPY ol-go121.repo /etc/yum.repos.d/
RUN sed -i s/mirror.centos.org/vault.centos.org/g /etc/yum.repos.d/*.repo && \
    sed -i s/^#.*baseurl=http/baseurl=http/g /etc/yum.repos.d/*.repo && \
    sed -i s/^mirrorlist=http/#mirrorlist=http/g /etc/yum.repos.d/*.repo
RUN yum -y install epel-release
RUN yum groupinstall -y 'Development Tools'
RUN yum install -y openssl-devel libuuid-devel wget squashfs-tools libarchive-devel golang which python36 cryptsetup
RUN yum install -y e2fsprogs fakeroot fuse-overlayfs fuse2fs squashfuse fuse3-devel
RUN yum -y install openssh-clients
#
# Final update and creation of the package list
RUN yum -y update && \
    echo "el7" > /build-platform && \
    rpm -qa > /var/lib/package-list
COPY build-singularity build-apptainer /bin/
