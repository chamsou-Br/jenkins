pipeline {
    agent any
    stages {
        stage ('build') {
            steps {
            bat 'gradle build'
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
             junit 'build/reports/**/*.xml'
            }
        }
        stage ('test') { // la phase build
            steps {
                bat 'gradle test'
            }
         }
    }
   

}
