pipeline {
    agent { label 'amazon-linux2' }

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
            steps {
                sh(script: 'docker images -a')
                sh(script: """
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                """)
            }
        }
        stage('Start test app') {
         steps {
            sh(script: """
               docker-compose up -d
               chmod 755 ./scripts/test_container.sh
               ./scripts/test_container.sh
            """)
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            sh(script: """
               pytest ./tests/test_sample.py
            """)
         }
      }
      stage('Stop test app') {
         steps {
            sh(script: """
               docker-compose down
            """)
         }
      }
    stage('Push container') {
        steps {
            echo "Workspace is $WORKSPACE"
            dir("$WORKSPACE/azure-vote") {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'DockerHub') {
                        def image = docker.build('danare/jenkins-course:latest')
                        image.push()
                    }
                }
            }
        }
    
    }
}
}
