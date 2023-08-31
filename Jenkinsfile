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
                    def image = docker.build('website-builder', '.')
                    if (env.BRANCH_NAME == 'master') {
                        sh "docker run -d -p 82:82 -v ${pwd()}:/var/www/html website-builder"
                    } else if (env.BRANCH_NAME == 'develop') {
                        sh "docker run --rm -v ${pwd()}:/var/www/html website-builder"
                    }
                }
            }
        }
    }
}

