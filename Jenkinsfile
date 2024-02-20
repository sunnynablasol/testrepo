pipeline{
  agent any
  environment{
    staging_server="165.227.223.121"
  }

  stages{
    stage('Deploy to Remote'){
      steps{
        sh 'scp ${WORKSPACE}/* clg-staging@${staging_server}:/srv/users/clg-staging/apps/ifebill/public/test/'
      }
    }
  }
}
