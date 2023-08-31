pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Publish') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'master') {
                        sh "docker build -t website-builder ."
                        sh "docker run -d -p 82:80 -v ${pwd()}:/var/www/html website-builder"
                    } else if (env.BRANCH_NAME == 'develop') {
                        sh "docker build -t website-builder ."
                    }
                }
            }
        }
    }
}
