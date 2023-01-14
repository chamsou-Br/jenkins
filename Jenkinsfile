pipeline {
    agent any
    stages {

        
        stage ('test') { // la phase build
            steps {
                bat 'gradle test'
               archiveArtifacts 'build/libs/*.jar'
                 junit 'build/reports/*.xml'
            }
         }




    }
   

}
