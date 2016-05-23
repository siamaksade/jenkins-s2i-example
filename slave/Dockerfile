# The FROM will be replaced when building in OpenShift
FROM rhel7/rhel

# Install headless Java
USER root
RUN curl -sL -o /tmp/epel-release-latest-7.noarch.rpm \
      https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    rpm -Uvh /tmp/epel-release-latest-7*.rpm && \
    export INSTALL_PKGS="nss_wrapper java-1.8.0-openjdk-headless \
      java-1.8.0-openjdk-devel nss_wrapper gettext tar git" && \
    yum clean all && \
    yum install -y --setopt=tsflags=nodocs install $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all && \
    mkdir -p /var/lib/jenkins && \
    chown -R 1001:0 /var/lib/jenkins && \
    chmod -R g+w /var/lib/jenkins

# Copy the entrypoint
COPY contrib/openshift/* /var/lib/jenkins/
USER 1001

# Run the JNLP client by default
# To use swarm client, specify "/var/lib/jenkins/run-swarm-client" as Command
ENTRYPOINT ["/var/lib/jenkins/run-jnlp-client"]
