pipeline {
  agent any
  stages {
    stage('Echo - Declarative') {
      when { branch pattern: "\\w+\\-pipeline", comparator: "REGEXP" }
      steps {
        echo 'This is a pipeline branch'
      }
    }
    stage('Echo - Scripted') {
      steps {
        script {
          if (env.BRANCH_NAME == 'master') {
            echo 'This is the master branch'
          } else {
            echo 'This is NOT the master branch'
          }
        }
      }
    }
  }
}