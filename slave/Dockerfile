# The FROM will be replaced when building in OpenShift
FROM rhel7/rhel

# Install headless Java
USER root
RUN curl -o /tmp/epel-release-latest-7.noarch.rpm https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    rpm -Uvh /tmp/epel-release-latest-7*.rpm && \
    export INSTALL_PKGS="nss_wrapper java-1.8.0-openjdk-headless java-1.8.0-openjdk-devel nss_wrapper" && \
    yum install -y --setopt=tsflags=nodocs install $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all && \
    mkdir -p /opt/app-root/jenkins && \
    chown -R 1001:0 /opt/app-root/jenkins && \
    chmod -R g+w /opt/app-root/jenkins

# Copy the entrypoint
COPY contrib/openshift/* /opt/app-root/jenkins/
USER 1001

# Run the JNLP client by default
# To use swarm client, specify "/opt/app-root/jenkins/run-swarm-client" as Command
ENTRYPOINT ["/opt/app-root/jenkins/run-jnlp-client"]
