pipeline {
    agent any
    
    stages {
        stage('GIT') {
            steps {
                echo "📥 Getting Project from Git"
                checkout scm
            }
        }
        
        stage('MVN CLEAN') {
            steps {
                echo "🧹 Nettoyage du projet"
                sh 'mvn clean'
            }
        }
        
        stage('MVN COMPILE') {
            steps {
                echo "🔨 Compilation du code"
                sh 'mvn compile'
            }
        }
        
        stage('MVN SONARQUBE') {
            steps {
                echo "📊 Analyse SonarQube"
                sh 'mvn sonar:sonar -Dsonar.projectKey=DevOpsProject -Dsonar.host.url=http://localhost:9000 -Dsonar.login=admin -Dsonar.password=Ahmed123/saadani'
            }
        }
        
        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        success {
            echo '✅ Build et analyse SonarQube réussis!'
        }
        failure {
            echo '❌ Build échoué!'
        }
    }
}
