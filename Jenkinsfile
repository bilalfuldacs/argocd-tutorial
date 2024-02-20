pipeline {
    agent any

    environment {
        APP_NAME = "complete-prodcution-e2e-pipeline"
        GITHUB_EMAIL = credentials('bilalfuldacs@gmail.com')
        GITHUB_PASSWORD = credentials('Ponkvscina@o11')
    }

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Git') {
            steps {
                git branch: 'main',
                    credentialsId: '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',
                    url: 'https://github.com/bilalfuldacs/argocd-tutorial.git'
            }
        }

        stage('Update the development tag') {
            steps {
                sh """
                cat quickstart-demo/deployment.yaml
                sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' quickstart-demo/deployment.yaml
                cat quickstart-demo/deployment.yaml
                """
            }
        }

        stage("Push to GitHub") {
            steps {
                // Set Git user name and email
                sh "git config --global user.email '${GITHUB_EMAIL}'"
                sh "git config --global user.password '${GITHUB_PASSWORD}'"
                
                // Add the changed file to the Git index
                sh "git add quickstart-demo/deployment.yaml"

                // Commit the changes
                sh "git commit -m 'updated yaml file'"

                // Push changes to GitHub
                sh "git push https://github.com/bilalfuldacs/argocd-tutorial.git main"
            }
        }
    }
}
