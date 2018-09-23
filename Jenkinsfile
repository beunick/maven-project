pipeline {
    agent any
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
    }
}
