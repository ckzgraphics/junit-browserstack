pipeline {

agent any

    environment {
        BROWSERSTACK_USERNAME = credentials('BROWSERSTACK_USERNAME')
        BROWSERSTACK_ACCESS_KEY = credentials('BROWSERSTACK_ACCESS_KEY')
    }
 
stages {
 
  stage('Cloning Git') {
    steps {
      git 'https://github.com/ckzgraphics/junit-browserstack'
    }
  }
 
 stage('Install dependencies') {
    steps {
        sh 'mvn compile'
    }
 }
 stage('Test') {
     steps {

browserstack('19ff12d1-a1d1-439c-8513-ed57a2cb287e') {
    sh 'mvn test -P single'
}
     }
  }      
}
 post { 
        always { 
            echo 'I will always say Hello again!'
            junit testDataPublishers: [[$class: 'AutomateTestDataPublisher']], testResults: 'target/surefire-reports/TEST-*.xml'
        }
    }
}