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
        
        stage('SonarQube'){
            steps{
                sh 'mvn sonar:sonar'
            }
        }
        stage('Jacoco Report'){
            steps{
                sh 'mvn test jacoco:report'  //  Uses existing config
            }
        }    
        
    }

       post {
            always {
                jacoco(
                     execPattern: '**/target/jacoco.exec',
                     classPattern: '**/target/classes/**/*.class',
                     sourcePattern: 'src/main/java/**/*.java',
                     exclusionPattern: 'src/test/**/*.java'
                     )
                  }
               }
}
