pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }
        
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
    }
    
    post {
        success {
            archiveArtifacts 'target/*.jar'
            echo '✅ Build réussi!'
        }
        failure {
            echo '❌ Build échoué!'
        }
    }
}
