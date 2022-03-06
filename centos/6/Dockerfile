FROM centos:6
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"

# Singularity build system
COPY CentOS-Base.repo /etc/yum.repos.d
RUN yum -y install epel-release && \
    yum groupinstall -y 'Development Tools' && \
    yum install -y openssl-devel libuuid-devel wget squashfs-tools libarchive-devel golang which python36 cryptsetup && \
    yum -y install openssh-clients && \
    #
    # Final update and creation of the package list
    yum -y update && \
    echo "el6" > /build-platform && \
    rpm -qa > /var/lib/package-list
COPY build-singularity /bin/
