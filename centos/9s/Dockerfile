FROM quay.io/centos/centos:stream9
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"

# Singularity build system
RUN dnf groupinstall -y 'Development Tools' && \
    dnf install -y openssl-devel libuuid-devel wget squashfs-tools golang which python cryptsetup && \
    dnf -y install openssh-clients && \
    #
    # Final update and creation of the package list
    dnf -y update && \
    echo "el9" > /build-platform && \
    rpm -qa > /var/lib/package-list
COPY build-singularity /bin
