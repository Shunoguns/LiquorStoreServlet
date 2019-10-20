pipeline {
    agent any

    stages {
         stage ('Checking Deploy tool and initial cleanup') {
             steps {
                 sh 'mvn --version'
                 sh 'java -version'
                 sh ' git --version'
             }
         }

         stage ('compile and test code') {
             steps  {
                 sh 'mvn clean install'
             }
         }
         stage ('deploy code to App Server') {
             steps  {
                 echo  'deployed'
                 sh ' cp /tmp/key.pem jenkinskey3.pem && chmod 400  jenkinskey3.pem'
                 sh 'scp -i  jenkinskey3.pem -o StrictHostKeyChecking=no target/SampleServlet.war  ec2-user@172.31.12.75:/var/lib/tomcat/webapps'
             }
        }
        stage ('Test code on App Server') {
             steps  {
                 echo  'code tested'
             }
        }
        stage ('complete') {
             steps  {
                 echo  'complete'
            }
        }
    }
}
