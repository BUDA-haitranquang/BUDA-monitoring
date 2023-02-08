FROM jenkins/jenkins:lts
COPY --chown=jenkins:jenkins certificate.pfx /var/lib/jenkins/certificate.pfx
COPY --chown=jenkins:jenkins private_key.key /var/lib/jenkins/pk
ENV JENKINS_OPTS --httpPort=8080 --httpsPort=8443 --httpsKeyStore=/var/lib/jenkins/certificate.pfx --httpsKeyStorePassword=haitran
EXPOSE 8083