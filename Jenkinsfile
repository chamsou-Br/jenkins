pipeline {
    agent any
    stages {
        stage ('test') { // la phase build
            steps {
                bat 'gradle test'
            }
         }
    }
    
      post {
        always {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
            junit 'build/reports/**/*.xml'
        }
    }

}
