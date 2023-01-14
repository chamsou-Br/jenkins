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
                        [key: 'Commit', value: '<a href="${GERRIT_CHANGE_URL}">${GERRIT_PATCHSET_REVISION}</a>'],
                        [key: 'Submitter', value: '${GERRIT_PATCHSET_UPLOADER_NAME}']
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

   


