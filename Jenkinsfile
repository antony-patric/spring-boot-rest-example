timestamps {
    node {
        stage('Build') {
            checkout scm
            sh "mvn versions:set -DnewVersion=1.0.${env.BUILD_NUMBER} versions:commit"
            sh "mvn clean package -DskipTests"
        }
        
        stage('Publish') {
            sshagent(['private-ssh-key']) {
                sh '''
                    ssh -o StrictHostKeyChecking=no -l jenkins 192.168.0.20 java -version"
                    uptime
                    java -version
                    "
                    '''
                sh "java -version"
                sh "uptime"
                sh "scp target/spring-boot-rest-example-1.0.${env.BUILD_NUMBER}.war jenkins@192.168.0.20:/opt/spring/sample/staging"
            }
        }
    }
}