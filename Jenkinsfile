pipeline{
    agent any
    tools{
        maven 'LocalMaven'
    }
    stages{
        stage('build'){
            steps{
                sh " mvn clean package"
        }
    }
}
}