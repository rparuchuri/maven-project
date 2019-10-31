pipeline{
    agent any
    tools{
        maven 'LocalMaven'
    }
    stages{
        stage('build'){
            steps{
                sh " mvn clean package"
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
        }
    }
}
}