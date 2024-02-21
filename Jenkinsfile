pipeline {
  agent any
  environment {
    staging_server = "165.227.223.121"
  }

  stages {
    stage('Deploy to Remote') {
      steps {
        script {
          // Define the credentials ID for the private key
          def credentialsId = 'JenkinsServer-Private-Key'

          // Use withCredentials block to securely handle the private key
          withCredentials([sshUserPrivateKey(credentialsId: credentialsId, keyFileVariable: 'SSH_PRIVATE_KEY')]) {
            // Set the environment variable for the private key file path
            env.SSH_PRIVATE_KEY = SSH_PRIVATE_KEY

            // Use SSH agent to execute the rsync command with the private key
            sshagent(['JenkinsServer-Private-Key']) {
              // Define the source directory (local workspace) and destination directory on the remote server
              def sourceDir = "${WORKSPACE}/"
              def destinationDir = "clg-staging@${staging_server}:/srv/users/clg-staging/apps/ifebill/public/test/"

              // Execute rsync command to sync changes from source to destination
              sh "rsync -e 'ssh -i ${SSH_PRIVATE_KEY}' -avz --delete ${sourceDir} ${destinationDir}"
            }
          }
        }
      }
    }
  }
}
