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
                    sh "${tool('sonar-scanner')}/bin/sonar-scanner"
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
       stage('Publish to JFrog') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'artifactory-creds',
                    usernameVariable: 'JFROG_USER',
                    passwordVariable: 'JFROG_TOKEN'
                )]) {
                    sh '''
                        zip -r javascript-demo-${BUILD_NUMBER}.zip . -x "*.git*" -x "node_modules/*"
                        curl -u $JFROG_USER:$JFROG_TOKEN -T javascript-demo-${BUILD_NUMBER}.zip "http://13.201.51.61:8082//artifactory/javascript-artifacts/javascript-demo-${BUILD_NUMBER}.zip"
                    '''
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