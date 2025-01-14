pipeline { agent any

tools {
    maven 'M3'
}

environment {
    SCANNER_HOME = tool 'sonar-scanner'
}

stages {
    stage('Checkout') {
        steps {
            git branch: 'main', url: 'https://github.com/amoghazy/techgame'
        }
    }
    
  stage('Compile') {
        steps {
           sh "mvn clean compile"
        }
    }
    
    stage('Test cases') {
        steps {
           sh "mvn test"
        }
    }
    

    
    stage('SonarQube Analysis') {
       steps {
              withSonarQubeEnv('sonar-server') {
    
           sh ''' $SCANNER_HOME/bin/sonar-scanner  -Dsonar.projectName=techgame \
                -Dsonar.java.binaries=. \
                -Dsonar.projectKey=techgame \
                -Dsonar.jacoco.reportPath=target/jacoco.exec  \
               
                '''
      }
        }
    }
    
  
}}
