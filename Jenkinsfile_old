pipeline{
    agent any
        tools {
        maven 'LocalMaven'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo 'Now Archiving'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy-to-staging'){
            steps{
                build job: 'deploytostaging'
            }
        }
        stage('Deply-to-ptod'){
            steps{
                timeout(time:5, unit:'MINUTES'){
                    input message:'Approve production Deploy?'
                }
                build job: 'prod-deploy'
            }
            post{
                success{
                    echo 'Code deployed to Production'
                }
                failure{
                    echo 'Deplyment failed'
                }
            }
        }
    }
}