pipeline {
        agent any
        stages {
                stage('Compile'){
            steps{
                sh script: 'mvn clean -U compile'
                sh script: 'mvn clean install -X'
            }
        }
          stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('SonarQube Scanner') {
                      sh 'mvn package sonar:sonar'
              }
            }
          }
          stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
        }
      }
