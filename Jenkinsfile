pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Publish') {
            when {
                anyOf {
                    branch 'master'
                    branch 'develop'
                }
            }

            steps {
                script {
                    def image = docker.build('website-builder', '.')
                    if (env.BRANCH_NAME == 'master') {
                        image.run("-p 82:82 -v \$(pwd):/var/www/html -d")
                    } else if (env.BRANCH_NAME == 'develop') {
                        // Only build, no publish for develop branch
                        image.inside('-v \$(pwd):/var/www/html') {
                            // Do additional tasks if needed
                        }
                    }
                }
            }
        }
    }
}
