pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                withMaven {
                    sh 'cd research'
                    sh 'mvn -f ./research/pom.xml -B -DskipTests clean package' 
                }
            }
        }

        stage('Push code') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: '<Publish over SSH config>', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 1200000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: './', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }

        stage('Build on Remote') {
            steps{
                script{
                    def remote = [:]
                    remote.name = '<Easy to remember name>'
                    remote.host = '<IP address/Host name>'
                    remote.user = '<username>'
                    remote.identityFile = '<Path to identity file>'
                    remote.allowAnyHosts = true
                    sshCommand remote: remote, command: "<Execute command>"   
                }
            }
        }
    }
}