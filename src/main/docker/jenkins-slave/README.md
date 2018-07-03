# Usage of Jenkins Slave Image in Openshift:

Add to your `Jenkinsfile` the following code:

```.groovy
    podTemplate(label: "citrus",
            cloud: "openshift",
            inheritFrom: "maven",
            containers: [
                    containerTemplate(name: "jnlp",
                            image: "toschneck/citrus-jenkins-slave",
                    )
            ])
            {
                node('citrus') {
                    sh "echo execute oc citrus build"
                    checkout scm
                    sh "mvn install"
                    junit 'citrus-tests/target/citrus-reports/**/*.xml'
                    archiveArtifacts "citrus-tests/target/citrus-*/**/*"
                }
            }
```

For more details how to configure a `containerTemplate`, see the documentations:
 * [kubernetes-plugin - Container Configuration](https://github.com/jenkinsci/kubernetes-plugin/blob/master/README.md#container-configuration), 
 * [OpenShift - Example BuildConfig using the Jenkins Kubernetes Plug-in](https://docs.openshift.org/latest/using_images/other_images/jenkins.html#using-the-jenkins-kubernetes-plug-in)