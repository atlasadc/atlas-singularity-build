FROM almalinux:9
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"

# Singularity build system
RUN dnf groupinstall -y 'Development Tools'
RUN dnf install -y epel-release
RUN dnf config-manager --set-enabled crb
RUN dnf -y install openssl-devel libuuid-devel wget squashfs-tools golang which python cryptsetup
RUN dnf -y install openssh-clients e2fsprogs fakeroot fuse-overlayfs squashfuse fuse3-devel
#
# Final update and creation of the package list
RUN dnf -y update && \
    echo "el9" > /build-platform && \
    rpm -qa > /var/lib/package-list
COPY build-singularity build-apptainer /bin/
