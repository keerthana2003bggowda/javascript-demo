pipeline {
    agent { label 'javascript' }

    // triggers {
    //     pollSCM('H/1 * * * *')   // checks GitHub every 1 minute
    // }

    stages {

        stage('Checkout Code') {
            steps {
                
                git branch: 'main',
                    credentialsId: 'github-pat',
                    url: 'https://github.com/keerthana2003bggowda/javascript-demo.git'
            }
        }

        stage('Build') {
            steps {
                nodejs(nodeJSInstallationName: 'nodejs24.16.0') {
                    sh "npm install"
                    sh "nohup npm start &"
                }
            }
        }

        // stage('Run App') {
        //     steps {
        //         sh "npm start"
        //     }
        // }


    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}