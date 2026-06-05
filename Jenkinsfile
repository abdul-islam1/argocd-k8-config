pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', description: 'Enter the image tag to be used for deployment')
    }
    stages {
        stage('Update Image Tag') {
            steps {
                echo "Updating image tag to ${IMAGE_TAG}"
                sh 'cat ./k8s/deployment.yaml'
                sh "sed -i 's/jenkins-test.*/jenkins-test:${IMAGE_TAG}/g' ./k8s/deployment.yaml"
                sh 'cat ./k8s/deployment.yaml'
            }
        }
        stage('Push to Github') {
            steps {
                sh 'git config --global user.email abdul.islam1120@gmail.com'
                sh 'git config --global user.name abdul-islam1'
                sh 'git checkout main'
                sh 'git add ./k8s/deployment.yaml'
                sh "git commit -m 'Updated image tag to ${IMAGE_TAG}'"
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh 'git push https://${username}:${password}@github.com/abdul-islam1/argocd-k8-config.git main'
                        }
            }
        }
    }
}
