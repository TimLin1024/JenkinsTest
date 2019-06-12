//Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Deploy') {
            steps {
                //重复执行三次
                retry(3) {
                    // sh './flakey-deploy.sh'
                    sh 'echo "flakey-deploy"'
                }
                //设置超时
                timeout(time: 1, unit: 'MINUTES') {
                    // sh './health-check.sh'
                    sh 'echo "health check"'
                }
            }
        }
    }
    post{
      always {
        echo 'This is always run'
      }
      success{
        echo 'This will run only if successful'
      }
      failure {
        echo 'This will run only if failed'
      }
      unstable {
        echo 'This will run only if the run was marked as unstable'
      }      
      changed {
          echo 'This will run only if the state of the Pipeline has changed'
          echo 'For example, if the Pipeline was previously failing but is now successful'
      }      
    }
}