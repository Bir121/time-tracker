pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '*/target/.war'
                }
            }
        }

        stage ('Deployments'){
                    steps {
                       sshagent(['tomcat']) {
       sh "scp -v -o StrictHostKeyChecking=no */target/.war ec2-user@13.233.117.239:/opt/tomcat/webapps"

}
                    }
                }
            }
        }
