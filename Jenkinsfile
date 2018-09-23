pipeline {
    agent any

    tools{
        maven 'localMaven'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to staging') {
            steps {
                build job: 'deploy-to-staging' // It is a function of the pipeline that we can use to trigger a Job in Jenkins
            }
        }

        stage ('Deploy to production'){
            steps{
                timeout(time:5, unit: 'DAYS'){
                    input message: 'Approve Production Deployment'
                }
                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo 'Code deployed to production'
                }
                failure {
                    echo 'Deployment failed.'
                }
            }
        }
    }
}
