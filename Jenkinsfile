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
        sh "echo 'Hello World'"
      }
    }
  }

  post { 
    always {
      step([$class: 'GitHubCommitStatusSetter', 'reposSource': [$class: 'AnyDefinedRepositorySource']])
    }
  }
}
