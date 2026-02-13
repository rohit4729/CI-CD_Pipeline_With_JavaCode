pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    stages {
        // 1. ADDED: Checkout Stage to download the code
        stage("Checkout Code") {
            steps {
                // TODO: Put your actual Git URL here
                git branch: 'main', url: 'https://github.com/YOUR-USERNAME/YOUR-REPO.git'
            }
        }

        stage("Test") {
            steps {
                sh "mvn test"
            }
        }

        stage("Build") {
            steps {
                sh "mvn package"
            }
        }

        stage("Deploy on Test") {
            steps {
                // Ensure the 'Deploy to container' plugin is installed for this to work
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat9', path: '', url: 'http://35.154.157.215:8080')], contextPath: '/app', war: '**/*.war'
            }   
        }

        stage("Deploy on prod") {
            steps {
                 deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat9', path: '', url: 'http://13.127.240.55:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    
    post {
        always {
            echo "========always========"
        }
        success {
            echo "========pipeline executed successfully========"
        }
        failure {
            echo "========pipeline execution failed========"
        }
    }
}