FROM centos:7
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"

# Singularity build system
RUN if [ "$TARGETPLATFORM" == "linux/arm64" ] ; then \
      cat > /etc/yum.repos.d/go116.repo <<EOD
[go116]
name=Oracle Linux 7 (aarch64) Go Language 1.16 for Development - \$basearch
baseurl=http://yum.oracle.com/repo/OracleLinux/OL7/developer/golang116/\$basearch
failovermethod=priority
enabled=1
gpgcheck=0
EOD
    fi
RUN yum -y install epel-release && \
    yum groupinstall -y 'Development Tools' && \
    yum install -y openssl-devel libuuid-devel wget squashfs-tools libarchive-devel golang which python36 cryptsetup && \
    yum -y install openssh-clients && \
    #
    # Final update and creation of the package list
    yum -y update && \
    echo "el7" > /build-platform && \
    rpm -qa > /var/lib/package-list
COPY build-singularity build-apptainer /bin/
