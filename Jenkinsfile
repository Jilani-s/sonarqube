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
                      sh 'mvn sonar:sonar -Dsonar.login=b8955d9ed743feb2c0fcbb2fa30532ec1489ba09'
                      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
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
