FROM centos:7
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"
ENV GOVER=1.24.3

# Singularity build system
RUN sed -i s/mirror.centos.org/vault.centos.org/g /etc/yum.repos.d/*.repo && \
    sed -i s/^#.*baseurl=http/baseurl=http/g /etc/yum.repos.d/*.repo && \
    sed -i s/^mirrorlist=http/#mirrorlist=http/g /etc/yum.repos.d/*.repo
RUN yum -y install epel-release
RUN yum groupinstall -y 'Development Tools'
RUN yum install -y openssl-devel libuuid-devel wget squashfs-tools libarchive-devel which python36 cryptsetup
RUN yum install -y e2fsprogs fakeroot fuse-overlayfs fuse2fs squashfuse fuse3-devel
RUN yum install -y lz4-devel lzo-devel xz-devel libzstd-devel
RUN yum -y install openssh-clients
RUN if [ "$TARGETPLATFORM" == "linux/amd64" ] ; then \
      cd /opt && \
      wget https://go.dev/dl/go${GOVER}.linux-amd64.tar.gz \
    ; else \
      cd /opt && \
      wget https://go.dev/dl/go${GOVER}.linux-arm64.tar.gz \
    ; fi 
RUN cd /opt && \
    tar xfz go${GOVER}.linux-*.tar.gz && \
    rm -fr go${GOVER}.linux-*.tar.gz && \
    echo "export PATH=/opt/go/bin:$PATH" >> /etc/profile.d/go.sh
#
# Final update and creation of the package list
RUN yum -y update && \
    echo "el7" > /build-platform && \
    rpm -qa > /var/lib/package-list
COPY build-singularity build-apptainer /bin/
