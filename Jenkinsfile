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

      stage('NEXUS'){
            steps{
                sh 'mvn deploy'
            }
        }
        

       stage('deploy to tomcat'){
           steps{
                sshagent(['vagrant-ssh']) {
                     sh '''
                echo "Starting WAR file transfer..."
                scp -v -o StrictHostKeyChecking=no target/Pipeline-Project.war vagrant@192.168.33.11:/opt/tomcat/webapps/
                echo "WAR file successfully deployed!"
            '''
                    
                    }
             } 
       }

        
    }

       post {
        always {
            junit 'target/surefire-reports/*.xml'  // Publish test results
            jacoco(
                execPattern: 'target/jacoco.exec',
                classPattern: 'target/classes/**/*.class',
                sourcePattern: 'src/main/java/**/*.java',
                exclusionPattern: 'src/test/**/*.java'
            )
        }
    }
}
    


