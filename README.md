### Jenkins S2I Example

An example demonstrating Jenkins S2I features for installing plugins, configuring jobs, Jenkins, etc


# Instructions
$ oc new-app jenkins~https://github.com/siamaksade/jenkins-s2i-example.git --name=ci-jenkins
$ oc expose svc/ci-jenkins --name=jenkins
