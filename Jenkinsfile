def updateJobStatus() {
  step([$class: 'GitHubCommitStatusSetter', 'reposSource': [$class: 'ManuallyEnteredRepositorySource', url: GIT_URL]])
}
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
        updateJobStatus()
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
      updateJobStatus()
    }
  }
}
