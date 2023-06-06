pipeline {
  agent {
    node {
      label 'windows'
    }

  }
  stages {
    stage('Build') {
      steps {
        echo 'Build Demo Application'
      }
    }

    stage('Linux Test') {
      parallel {
        stage('Linux Test') {
          steps {
            sh 'sh run_build_script.sh'
          }
        }

        stage('Windows Test') {
          steps {
            echo 'run windows tests'
          }
        }

      }
    }

    stage('Deploy staging') {
      steps {
        echo 'Deploy to staging environment'
        input 'Ok deploy ? '
      }
    }

    stage('Deploy Production ') {
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'YOUR EMAIL ADDRESS', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}