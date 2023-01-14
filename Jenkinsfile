pipeline {
    agent any
    stages {
        stage ('test') { // la phase build
            steps {
                bat 'gradle test'
                archiveArtifacts 'build/test-results/'
            }
            
         }
        
        
        
          stage ('Code Analysis') { // la phase build
            steps {
                                withSonarQubeEnv('sonar'){
                bat 'gradle sonarqube'
                                }
            }
         }
          stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
                  stage("Build") {
            steps {
                bat 'gradle build'
                bat 'gradle javadoc'
                archiveArtifacts 'build/libs/*.jar'
                archiveArtifacts 'build/docs/'
            }
        }
             stage("deploy") {
            steps {
                bat 'gradle publish'

            }
        }
    }
     post {
    success {
        slackSend channel: '#Tp_gradle',
                  color: 'good',
                  message: "The pipeline completed successfully."
    }
}
   

}
