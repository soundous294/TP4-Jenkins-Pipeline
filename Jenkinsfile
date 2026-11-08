
pipeline {
    agent any

    tools {
        jdk 'JDK21'
    }

    parameters {
        choice(
            name: 'DEPLOY_ENV',
            choices: ['Development', 'Production'],
            description: 'Choose deployment environment'
        )
    }

    environment {
        APP_NAME = 'MyApplication'
        VERSION = '1.0'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"
                echo "Version: ${VERSION}"
            }
        }

        stage('Test') {
            steps {
                echo "Testing ${APP_NAME}"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying ${APP_NAME} to ${params.DEPLOY_ENV}"
            }
        }

        stage('External Groovy Script') {
            steps {
                script {
                    def externalScript = load 'script.groovy'

                    echo externalScript.getMessage()
                    echo externalScript.showDeployment(params.DEPLOY_ENV)
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
