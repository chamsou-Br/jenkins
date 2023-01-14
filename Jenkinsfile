pipeline {
    agent any
    stages {

        
        stage ('test') { // la phase build
            steps {
                bat 'gradle test'
                archiveArtifacts 'build/libs/*.jar'
                junit 'build/test-results/test/TEST-Matrix.xml'
            }
         }
        
          stage ('Code Analysis') { // la phase build
            steps {
                bat 'gradle sonarqube'
            }
         }




    }
   

}
