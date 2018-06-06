FROM consol/citrus:2.7.5

MAINTAINER citrusframework.org <citrus-dev-l@consol.de>

ENV BUILD_DATE=2018-06-06

### sourced are copied from:
# https://github.com/openshift/jenkins/tree/master/slave-base
# https://github.com/openshift/jenkins/tree/master/slave-maven

# Copy the jenkins-slave entrypoint
ADD contrib/bin/* /usr/local/bin/

# Run the Jenkins JNLP client
ENTRYPOINT ["/usr/local/bin/run-jnlp-client"]
