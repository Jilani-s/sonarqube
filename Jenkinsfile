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
                      sh 'mvn clean install'
                      sh 'mvn sonar:sonar \
  -Dsonar.projectKey=POC-project \
  -Dsonar.host.url=http://3.87.22.107:9000 \
  -Dsonar.login=75183a7a6835a919d07dbeb85419f3e41aa26745'
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
