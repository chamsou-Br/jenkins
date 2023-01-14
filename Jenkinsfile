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
                archiveArtifacts 'build/docs/javadoc/*.html'
            }
        }
             stage("deploy") {
            steps {
                bat 'gradle publish'

            }
        }
        




    }
   

}
