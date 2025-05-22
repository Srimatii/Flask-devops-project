pipeline {
    agent any
    stages {
       // stage('Clone Repo') {
         //   steps {
           //     git 'https://github.com/yourusername/devops-flask-app.git'
            //}
        //}
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("flask-devops-project")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-credentials', url: '']) {
                    sh 'docker tag flask-devops yourdockerhub/flask-devops:latest'
                    sh 'docker push yourdockerhub/flask-devops:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}
