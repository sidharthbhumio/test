pipeline {

  agent {
    kubernetes {
      cloud 'kubernetes'
      inheritFrom 'kaniko'
      namespace 'jenkins'
    }
  }
  
  stages {
    stage("Update Commit Status As Pending") {
      steps {
        step([$class: 'GitHubSetCommitStatusBuilder'])
      }
    }

    stage("Wait for 10 seconds") {
      steps {
        sleep 10
      }
    }

    stage("Job") {
      steps {
        sh "echo '${GIT_URL}'"
      }
    }
  }

  post { 
    always {
      step([$class: 'GitHubCommitStatusSetter', 'reposSource': [$class: 'ManuallyEnteredRepositorySource', url: '${GIT_URL}']])
    }
  }
}
