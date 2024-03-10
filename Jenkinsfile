pipeline {
    agent any

    stages {
        stage('Deploy PHP Application') {
            steps {
                script {
                    // Skip karne ke liye folder paths
                    def skippedFolders = ['skip1', 'skip2']
                    // Remote directory
                    def remoteDir = '/srv/users/clg-staging/apps/ifebill/public/test/'

                    sshPublisher(
                        publishers: [sshPublisherDesc(
                            configName: 'CLG-Staging-CI-IFEBILL',
                            transfers: [sshTransfer(
                                cleanRemote: false,
                                execCommand: '',
                                execTimeout: 120000,
                                flatten: false,
                                makeEmptyDirs: false,
                                noDefaultExcludes: false,
                                patternSeparator: '[, ]+',
                                remoteDirectory: remoteDir,
                                remoteDirectorySDF: false,
                                removePrefix: '',
                                sourceFiles: "**/*.html, **/*.css, **/*.php, **/*.js, !{skippedFolders.join(',')}" 
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
