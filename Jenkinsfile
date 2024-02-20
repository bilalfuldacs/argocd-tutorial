pipeline {
    agent any

    
    environment {
        APP_NAME = "complete-prodcution-e2e-pipeline"
       
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
        sh "git config --global user.name 'bilalfuldacs'"
        sh "git config --global user.email 'bilalfuldacs@gmail.com'"

        // Add the changed file to the Git index
        sh "git add quickstart-demo/deployment.yaml"

        // Commit the changes
        sh "git commit -m 'updated yaml file'"

        // Push the changes to GitHub
        withCredentials([gitUsernamePassword(credentialsId: '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', gitToolName: 'Default')]) {
            sh "git push https://github.com/bilalfuldacs/argocd-tutorial.git main"
        }
    }
}

    

    
    }
}
