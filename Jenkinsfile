pipeline {
    agent any
    
    tools {
        maven 'MAVEN'
    }

    stages {
        stage('checkout') {
            steps {
                echo 'Getting the project'
                git branch:'main',url: 'https://github.com/Coding4Deep/jenkins-pipelines.git'
            }
        }
        stage('BUILD') {
            steps {
                echo 'Building the project'
                sh 'mvn clean package'
            }
        }

         stage('Jacoco Report'){
            steps{
                sh 'mvn test jacoco:report'  
            }
        }
        
        stage('SonarQube'){
            steps{
                sh 'mvn sonar:sonar'
            }
        }
           
        
    }

        post {
            success {
                    publishHTML(target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'target/site/jacoco',
                        reportFiles: 'index.html',
                        reportName: 'JaCoCo Code Coverage Report'
                    ])
                }
            }
        }
    

}
