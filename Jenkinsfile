podTemplate(label: 'jenkins-pipeline', containers: [
    containerTemplate(name: 'jnlp', image: 'jenkins/jnlp-slave:3.10-1', args: '${computer.jnlpmac} ${computer.name}', workingDir: '/home/jenkins', resourceRequestCpu: '500m', resourceLimitCpu: '500m', resourceRequestMemory: '1024Mi', resourceLimitMemory: '1024Mi'),
    containerTemplate(name: 'docker', image: 'docker:1.12.6', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.3', command: 'cat', ttyEnabled: true)
],
volumes:[
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
]) {
    node ('jenkins-pipeline') {
         // checkout sources
        checkout scm
        
        stage ('Viewer') {
            container('docker') {
                stage ('Build viewer') {
                    sh 'docker pull redis'
                }
            }
        }
    }
}
