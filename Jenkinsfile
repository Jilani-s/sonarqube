pipeline {
        agent any
        stages {
                stage('Compile'){
            steps{
                sh script: 'mvn clean -U compile -s settings.xml'
                
            }
        }
          stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('SonarQube Scanner') {
                      withMaven(maven:'Maven 3.6.3') {
                      sh 'mvn clean verify sonar:sonar'
              }
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
