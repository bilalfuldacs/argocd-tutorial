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

        stage('pushed the changed deployment') {
             steps {
                withCredentials([usernamePassword(credentialsId: 'github', usernameVariable: 'GITHUB_USERNAME', passwordVariable: 'GITHUB_PASSWORD')]) {
    sh """
    git config --global user.name "bilalfuldacs"
    git config --global user.email "bilalfuldacs@gmail.com"
    git add quickstart-demo/deployment.yaml
    git commit -m "updated yaml file"
    git push https://${GITHUB_USERNAME}:${GITHUB_PASSWORD}@github.com/bilalfuldacs/argocd-tutorial.git main
    """
}


            }
        }
    

    
    }
}
