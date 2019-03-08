timestamps {
    node {
        stage('Build') {
            checkout scm
            sh "mvn versions:set -DnewVersion=1.0.${env.BUILD_NUMBER} versions:commit"
            sh "mvn clean package"
        }
        
        stage('Publish') {
            sshagent(['private-ssh-key']) {
                sh '''
                    ssh -o StrictHostKeyChecking=no -l jenkins 192.168.0.20"
                    uptime
                    java -version
                    "
                    '''
            }
        }
    }
}