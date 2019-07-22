FROM centos:7
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"

# Singularity build system
RUN yum -y install epel-release && \
    yum groupinstall -y 'Development Tools' && \
    yum install -y openssl-devel libuuid-devel libseccomp-devel wget squashfs-tools golang && \
    yum -y install openssh-clients && \
    #
    # Final update and creation of the package list
    yum -y update && \
    rpm -qa > /var/lib/package-list
COPY build-singularity /bin
