pipeline {
  agent any
  environment {
    staging_server = "165.227.223.121"
  }

  stages {
    stage('Deploy to Remote') {
      steps {
        script {
          
          def credentialsId = 'JenkinsServer-Private-Key'

          // Use withCredentials block to securely handle the private key
          withCredentials([sshUserPrivateKey(credentialsId: credentialsId, keyFileVariable: 'SSH_PRIVATE_KEY')]) {
            // Set the environment variable for the private key file path
            env.SSH_PRIVATE_KEY = SSH_PRIVATE_KEY

            // Use SSH agent to execute the scp command with the private key
            sshagent(['JenkinsServer-Private-Key']) {
              sh "scp -i ${SSH_PRIVATE_KEY} ${WORKSPACE}/* clg-staging@${staging_server}:/srv/users/clg-staging/apps/ifebill/public/test/"
            }
          }
        }
      }
    }
  }
}
