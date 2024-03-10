pipeline {
    agent any

    stages {
        stage('Deploye PHP Application') {
            steps {
                script {
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
                                remoteDirectory: '/srv/users/clg-staging/apps/ifebill/public/test/',
                                remoteDirectorySDF: false,
                                removePrefix: '',
                                sourceFiles: '/.html, **/.css, */.php, */.js',
                                excludedFiles: 'skip1//, skip2//' // Skip folder1 and folder2
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
