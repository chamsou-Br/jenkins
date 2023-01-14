pipeline {
    agent any
    stages {
        stage ('build') {
            steps {
            bat 'gradle build'
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
            }
        }
        stage ('test') { // la phase build
            steps {
                bat 'gradle test'
            }
         }
    }
   

}
