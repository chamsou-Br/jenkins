pipeline {
    agent any
    stages {

        
        stage ('test') { // la phase build
            steps {
                bat 'gradle test'
               archiveArtifacts 'build/libs/*.jar'
                cucumber buildStatus "UNSTABLE",
                         reportTitle :  "Cucumber",
                         fileIncludePattern : "target/report.json",
            }
         }
        
          stage ('Code Analysis') { // la phase build
            steps {
                bat 'gradle sonarqube'
            }
         }




    }
   

}
