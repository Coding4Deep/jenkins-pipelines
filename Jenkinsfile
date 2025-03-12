
node {
    
    // Define Maven tool and store its path
    def MVN = tool name: "MAVEN"
    def remoteServer = "vagrant@192.168.33.11"
    def warFile = "target/local-project.war"
    def remotePath = "/opt/tomcat/webapps/"
    
    stage('Fetch') {
        git branch:'main',url: 'https://github.com/Coding4Deep/JENKINS.git'
    }
    
    stage('Build') {
        sh "$MVN/bin/mvn clean package"
    }
    
   stage('SonarQube') {
            sh "$MVN/bin/mvn sonar:sonar"
   }
     stage('JaCoCo Report') {
        sh "$MVN/bin/mvn jacoco:report"
    }
    
  /*   stage('Upload to Nexus') {
        sh "$MVN/bin/mvn deploy"
    }  */
    
    stage('deploy to the tomcat'){
           sshagent(['vagrant-ssh']) {
               sh " scp ${warFile} ${remoteServer}:${remotePath}"
              }
        }

}
