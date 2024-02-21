pipeline {
    agent any

    stages {
        stage('Deploye PHP Application') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'CLG-Staging-CI-IFEBILL', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/srv/users/clg-staging/apps/ifebill/public/test/', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*.html')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
