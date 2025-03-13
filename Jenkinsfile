pipeline{
    agent any
tools{
    maven 'MAVEN'
}

    stages{
        stage('checkout'){
            steps{
                echo 'getting the project'
                git 'https://github.com/Coding4Deep/jenkins-pipelines.git'
            }
        }
        stage('BUILD'){
            steps{
                echo 'Building the project'
         }
   }
}
