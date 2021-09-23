pipeline {
    agent any

    options {
        timestamps() // Add timestamps to logging
        timeout(time: 2, unit: 'MINUTES') // Abort pipleine

        buildDiscarder(logRotator(numToKeepStr: '8', artifactNumToKeepStr: '8'))
        disableConcurrentBuilds()
    }
    environment {
        PATH = "/usr/local/bin:$PATH"
    }
    
    stages {

        stage('Set ID') {
            steps {
                echo 'Stage: Set ID'
                sh '''
                echo "DX20210101" > currentFile
                idtag=$(cat currentFile)
                echo "idtag=${idtag}"
                '''
                script {
                    def idtag = sh(script: "cat currentFile", returnStdout: true).trim()
                    echo "idtag: ${idtag}"
                    build(job: '/zAnalysisMgr/main', parameters: [string(name: 'idtag', value: "${idtag}")], wait: true)
                }
            }
        }
        
    }
    post {
        always {
            echo "post/always"
            deleteDir() // clean workspace
        }
        success {
            echo "post/success"
        }
        failure {
            echo "post/failure"
        }
    }
}
