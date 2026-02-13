pipeline{
    agent any
    tools {
        maven 'Maven' 
    }
    stages{
        stage("Test"){
            steps{
                // mvn test
               sh "mvn test"
            }
            
        }
        stage("Build"){
            steps{
                 
             sh "mvn package"
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -->plugin
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat9', path: '', url: 'http://35.154.157.215:8080')], contextPath: '/app', war: '**/*.war'
                
            }   
    }
        stage("Deploy on prod"){
            steps{
                // deploy on container -->plugin
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat9', path: '', url: 'http://13.127.240.55:8080')], contextPath: '/app', war: '**/*.war'
                
            }
            
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}