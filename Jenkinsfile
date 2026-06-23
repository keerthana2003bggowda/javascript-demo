pipeline {
    agent { label 'javascript' }

    

    stages {

        stage('Checkout Code') {
            steps {
                
                git branch: 'main',
                    credentialsId: 'github-pat',
                    url: 'https://github.com/keerthana2003bggowda/javascript-demo.git'
            }
        }
         stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                        sonar-scanner
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                nodejs(nodeJSInstallationName: 'nodejs24.16.0') {
                    sh "npm install"
                    sh " npm start &"
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