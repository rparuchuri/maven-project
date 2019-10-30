pipeline{
    agent any

    tools{
        maven'LocalMaven'
    }

    parameters{
         string(name: 'tomcat_stag', defaultValue: '34.238.157.103', description: 'staging server')
         string(name: 'tomcat_prod', defaultValue: '34.238.157.103', description: 'prod server')
    }

    triggers{
        pollSCM('* * * * *')
    }

stages{
    stage('Build'){
        steps {
            sh 'mvn clean package'
        }
        post{
            success{
                echo 'Now Archiving'
                archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }

    stage('Deployments'){
        parallel{
            stage('Deploy to staging'){
                steps{
                    sh "cp -i '/Users/rparuchuri/Downloads/jenkins.pem' **/target/*.war ec2_user@${params.tomcat_stag}:/var/tmp/apache-tomcat-8.5.47-stag/webapps"
                }
            }
            stage( 'Deploy to Prod'){
                steps{
                    sh "cp -i '/Users/rparuchuri/Downloads/jenkins.pem' **/target/*.war ec2_user@${params.tomcat_prod}:/var/tmp/apache-tomcat-8.5.47-prod/webapps"
                }
            }

        }
    }

}
}