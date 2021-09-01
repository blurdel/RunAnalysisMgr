import java.text.SimpleDateFormat
def idtag // dataset/analsys id

pipeline {
    agent any

    options {
        timestamps() // Add timestamps to logging
        timeout(time: 15, unit: 'HOURS') // Abort pipleine

        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
        disableConcurrentBuilds()
    }
    environment {
        PATH = "/usr/local/bin:$PATH"
    }
    
    stages {

        stage('XXX') {
            steps {
                echo 'Stage: XXX'
                idtag="DX20201"
                build(job: '/AnalysisMgr/main', parameters: [string(name: 'idtag', value: "${idtag}")], wait: true)
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
