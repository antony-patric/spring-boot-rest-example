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

        // echo "${env.JOB_STATUS}"
        // echo "after --"
        // echo env.JOB_STATUS
        echo sh(script: 'env|sort', returnStdout: true)
        stage("Print"){
            echo "${env.JOB_STATUS}"
        }
            
        }
        if("${env.BRANCH_NAME}"!="master"){
            echo "Non master branch. Returning - ${env.STAGE_NAME}"
            currentBuild.result = 'SUCCESS'
            return
        }
        
        stage("Publish"){
                echo "Publish stage"
                echo "${env.BUILD_NUMBER}"
                echo sh(script: 'env|sort', returnStdout: true)
                echo "${env.PWD}"
                echo "after"
                deploy([app: "spring-boot-rest-example", port: "9080", env: "staging"])
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