@Library("workflowlibs@master") _

import com.halo.ims.Application
import com.halo.ims.Utils

timestamps{
    node{
        imsSpec(){
            app = new Application(this, "ims")
            utils = new Utils(this)
            stage("Build"){
                echo "Build stage"
                utils.mvn()
            }

            
        }
        stage("Publish"){
                echo "Publish stage"
                echo "${env.BUILD_NUMBER}"
                echo sh(script: 'env|sort', returnStdout: true)
                echo "${env.PWD}"
                echo "after"
                deploy([app: "spring-boot-example"])
                // sshagent(['private-ssh-key']) {
                // sh "scp target/spring-boot-rest-example-1.0.${env.BUILD_NUMBER}.war jenkins@192.168.0.20:/opt/spring/sample/staging/spring-boot-rest-example.war"
                // }
            }
    }
}

// timestamps {
//     node {

//         app = new Application(this, "ims")
//         utils = new Utils(this)

//         stage('Build') {
//             checkout scm
//             log.info("Invoking mvn command")
//             utils.mvn()
//             // sh "mvn versions:set -DnewVersion=1.0.${env.BUILD_NUMBER} versions:commit"
//             // sh "mvn clean package -DskipTests"
//         }
        
//         stage('Publish') {
//             sshagent(['private-ssh-key']) {
//                 sh '''
//                     ssh -o StrictHostKeyChecking=no -l jenkins 192.168.0.20 java -version"
//                     uptime
//                     java -version
//                     "
//                     '''
//                 sh "java -version"
//                 sh "uptime"
//                 sh "scp target/spring-boot-rest-example-1.0.${env.BUILD_NUMBER}.war jenkins@192.168.0.20:/opt/spring/sample/staging"
//             }
//         }
//     }
// }