pipeline {

  agent any

  environment {
    GH_REPO = "https://api.github.com/repos/sidharthbhumio/test"
    GH_TOKEN = credentials("github-token") 
  }

  def updateCommitStatus(status, message) {
    sh '''curl -L \
        -X POST \
        -H "Accept: application/vnd.github+json" \
        -H "Authorization: Bearer ${}" \
        -H "X-GitHub-Api-Version: 2022-11-28" \
        ${GH_REPO}/statuses/${GIT_COMMIT}
        -d '{"state":${status},"target_url":"${BUILD_URL}","description":${message},"context":"continuous-integration/jenkins"}'''
  }

  stages {
    stage("Update Commit Status As Pending") {
      updateCommitStatus("pending", "The commit is being built")
    }

    stage("Wait for 10 seconds") {
      sleep 10
    }

    stage("Job") {
      sh "echo 'Hello World'"
    }
  }

  post { 
    success {
      updateCommitStatus("success", "The commit is built successfully!")
    }

    failure {
      updateCommitStatus("failure", "The commit is built successfully!")
    }
  }
}
