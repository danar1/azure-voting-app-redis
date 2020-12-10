node {
  stage('Echo on master') {
    if (env.BRANCH_NAME == 'master') {
      echo 'This is the master branch'
    } else {
      echo 'This is NOT the master branch'
    }
  }
}