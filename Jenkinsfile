pipeline {
    agent any
    stages {
        stage ('test') { // la phase build
            steps {
                bat 'gradle test'
                archiveArtifacts 'build/test-results/'
                cucumber buildStatus: 'STABLE',
                reportTitle: 'My report',
                fileIncludePattern: '**/*.json',
                trendsLimit: 10,
                classifications: [
                    [
                        'key': 'Browser',
                        'value': 'Firefox'
                    ]
                ]
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
                archiveArtifacts 'build/docs/'
            }
        }
             stage("deploy") {
            steps {
                bat 'gradle publish'

            }
        }
                         stage("notification") {
            steps {
                 notifyEvents message: 'Pipeline <b> is sucessufuly termined</b>', token: '3mD8_X1iRhMU2V88vV2lDJmefzwSu1-F'

            }
        }
    }

    }

   


