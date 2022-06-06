pipeline {
        agent any
    
    tools {
      maven 'Maven_3.5.4'
          }
        stages {
                stage('Compile'){
            steps{
                sh script: 'mvn clean -U compile'
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
