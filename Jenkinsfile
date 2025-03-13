pipeline {
    agent any
    
    tools {
        maven 'MAVEN'
    }

    stages {
        stage('checkout') {
            steps {
                echo 'Getting the project'
                git 'https://github.com/Coding4Deep/jenkins-pipelines.git'
            }
        }
        stage('BUILD') {
            steps {
                echo 'Building the project'
                sh 'mvn clean package'
            }
        }
    }
}
