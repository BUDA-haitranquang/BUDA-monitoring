pipeline {
    agent {
        docker {
            image 'node:16.16.0'
            args '-p 3000:3000'
        }
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git changelog: false, credentialsId: '<Git Credential on Jenkins>', poll: false, url: '<Git repository URL>'
                sh 'npm install'

            }
        }
        stage('Start') { 
            steps {
                sh 'npm run build'
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
