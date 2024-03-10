pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                // Git repository se source code download karne ke liye
                git branch: 'main', url: 'https://github.com/sunnynablasol/testrepo.git'
            }
        }
        stage('Deploy PHP Application') {
            steps {
                script {
                    // Git repository se source code download hua directory
                    def sourceDir = './' 

                    // Remote directory - 'test' folder ka path
                    def remoteDir = '/srv/users/clg-staging/apps/ifebill/public/test/'

                    // Exclude karne wale folders ka list
                    def excludedFolders = " --exclude=skip1/ --exclude=skip2/*"

                    // rsync command banao
                    def rsyncCommand = "rsync -avz ${excludedFolders} --include='*/' --include='*.html' --include='*.css' --include='*.php' --include='*.js' --exclude='*' ${sourceDir} ${remoteDir}"

                    // sshPublisher ke through rsync command ko execute karo
                    sshPublisher(
                        publishers: [sshPublisherDesc(
                            configName: 'CLG-Staging-CI-IFEBILL',
                            transfers: [sshTransfer(
                                cleanRemote: false,
                                execCommand: rsyncCommand,
                                execTimeout: 120000,
                                flatten: false,
                                makeEmptyDirs: false,
                                noDefaultExcludes: false,
                                patternSeparator: '[, ]+',
                                remoteDirectory: remoteDir,
                                remoteDirectorySDF: false,
                                removePrefix: ''
                            )],
                            usePromotionTimestamp: false,
                            useWorkspaceInPromotion: false,
                            verbose: false
                        )]
                    )
                }
            }
        }
    }
}
