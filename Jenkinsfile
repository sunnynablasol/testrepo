pipeline {
  agent any
  environment {
    staging_server = "165.227.223.121"
    ssh_private_key = credentials('JenkinsServer-Private-Key') // Specify your SSH private key credentials ID
  }

  stages {
    stage('Deploy to Remote') {
      steps {
        script {
          // Define the private key file path
          def privateKeyFile = "${env.JENKINS_HOME}/.ssh/${ssh_private_key}"

          // Execute the scp command using ssh with private key authentication
          sh "ssh -i ${privateKeyFile} clg-staging@${staging_server} 'rsync -avz ${WORKSPACE}/ clg-staging@${staging_server}:/srv/users/clg-staging/apps/ifebill/public/test/'"
        }
      }
    }
  }
}
