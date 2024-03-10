pipeline {
    agent any

    stages {
        stage('Deploy PHP Application') {
            steps {
                script {
                    // Production Server ko Update karein
                    updateProductionServer('skip1/', 'skip2/')
                }
            }
        }
    }
}

def updateProductionServer(String... excludedFolders) {
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
                sourceFiles: '**/*.html, **/*.css, **/*.php, **/*.js',
                excludes: excludedFolders.collect { it }.join(',') // Chhodi gayi folders ko exclude karein
            )],
            usePromotionTimestamp: false,
            useWorkspaceInPromotion: false,
            verbose: false
        )]
    )
}
