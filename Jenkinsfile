pipeline {
    agent any

    stages {
        stage('Deploy PHP Application') {
            steps {
                script {
                    // Remote directory
                    def remoteDir = '/srv/users/clg-staging/apps/ifebill/public/test/'

                    // rsync command banao
                    def rsyncCommand = "rsync -avz --exclude=skip1/ --exclude=skip2/ --include='*/' --include='*.html' --include='*.css' --include='*.php' --include='*.js' --exclude='*' ./ ${remoteDir}"

                    // sshPublisher ke through rsync command ko execute karo
                    sshPublisher(
                        publishers: [sshPublisherDesc(
                            configName: 'CLG-Staging-CI-IFEBILL',
                            transfers: [sshTransfer(
                                cleanRemote: false,
                                execCommand: rsyncCommand,
                                execTimeout: 600000,
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
