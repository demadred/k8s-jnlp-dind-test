podTemplate(label: 'jenkins-pipeline', containers: [
    containerTemplate(name: 'jnlp', image: ' jenkins/jnlp-slave:3.10-1', args: '${computer.jnlpmac} ${computer.name}', workingDir: '/home/jenkins', resourceRequestCpu: '500m', resourceLimitCpu: '500m', resourceRequestMemory: '1024Mi', resourceLimitMemory: '1024Mi'),
    containerTemplate(name: 'docker', image: 'docker:1.12.6', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'maven', image: 'maven:3.5.0-jdk-8', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'helm', image: 'lachlanevenson/k8s-helm:v2.6.1', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.3', command: 'cat', ttyEnabled: true)
],
volumes:[
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
],
envVars: [
    envVar(key: 'JNLP_PROTOCOL_OPTS', value: '-Dorg.jenkinsci.remoting.engine.JnlpProtocol3.disabled=false')
]) {
    node ('jenkins-pipeline') {
        stage 'Run a docker thing'
        container('docker') {
            stage 'Docker thing1'
            sh 'docker pull redis'
        }
    }
}
