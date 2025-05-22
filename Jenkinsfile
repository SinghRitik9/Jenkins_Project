pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '43.204.218.251', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ("Deploy to Staging"){
                    steps {
deploy adapters: [tomcat9(alternativeDeploymentContext: '', path: '', url: 'http://13.232.77.126:8080/')], contextPath: null, war: '**/*.war'                    }
                }
            }
        }
    }
}
