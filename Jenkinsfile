pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build process'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Test') {
      parallel {
        stage('Linux Test') {
          steps {
            echo 'Testing process'
          }
        }

        stage('Windows Test') {
          steps {
            echo 'Windows Process'
          }
        }

      }
    }

    stage('Deploying Staging') {
      steps {
        echo 'Deployment to staging environment'
        input 'Ok to deploy to produce'
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy to Production'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}