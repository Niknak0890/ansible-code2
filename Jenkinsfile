pipeline{
    agent any

    stages{
        stage('zip the file'){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
            }
        }
        stage('upload artifacts to jfrog'){
            steps{
              sh 'curl -uadmin:AP8PYxTpmnyMe26bsUvyihFH7Sz -T \
              ansible-${BUILD_ID}.zip \
              "http://100.26.177.176:8081/artifactory/ansible/ansible-${BUILD_ID}.zip"'
           }
        }
        stage('publish to ansible server'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible-server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'll', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/ec2-user', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'ansible-*.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}