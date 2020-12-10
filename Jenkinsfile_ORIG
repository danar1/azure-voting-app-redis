@Library('github.com/devbyaccident/demo-shared-pipeline') _

pipeline {
  agent any
  stages {
    stage('Call Library Hello-World Function') {
      steps {
        script {
          helloWorld()
        }
      }
    }
  }
}