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
                // sed -i 's/jenkins-test.*/jenkins-test:${IMAGE_TAG}/g' ./k8s/deployment.yaml
                sh 'cat ./k8s/deployment.yaml'
            }
        }
    }
}
