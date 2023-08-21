pipeline {

  agent any

  environment {
    GH_REPO = "https://api.github.com/repos/sidharthbhumio/test"
    GH_TOKEN = credentials("github-token") 
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
      step([$class: 'GitHubCommitStatusSetter'])
    }
  }
}
