pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('jenkins-sonarqube') {
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
    }
    
}
