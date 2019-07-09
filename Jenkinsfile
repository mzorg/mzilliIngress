pipeline {
    agent any
    environment {
        def Namespace = "default"
        def Namespace_dev = "develop"
        def imageTag_i = sh "git rev-parse --short HEAD > .git/commit-id"
        imageTag = readFile('.git/commit-id').trim()
    }
    stages {
        stage('Environment') {
            steps {
                sh 'git --version'
                echo "Branch: ${env.BRANCH_NAME}"
                sh 'docker -v'
                sh 'printenv'
            }
        }
        stage('Deploy on K8s for development'){
            // when {
            //     branch 'develop' 
            // }
            steps {
                sh "kubectl apply -f ./ingress-dev.yaml -n ${env.Namespace_dev}"
            }
        }
        stage('Deploy on K8s for production'){
            // when {
            //     branch 'master' 
            // }
            steps {
                sh "kubectl apply -f ./ingress.yaml -n ${env.Namespace}"
            }
        }

    }
}
