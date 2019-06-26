node {
    def Namespace = "default"
      try {
        stage('Checkout') {
            checkout scm
            sh "git rev-parse --short HEAD > .git/commit-id"
            imageTag= readFile('.git/commit-id').trim()
        }
        stage('Environment') {
            sh 'git --version'
            echo "Branch: ${env.BRANCH_NAME}"
            sh 'printenv'
        }
        stage('Deploy on K8s'){
            sh "kubectl apply -f ./ingress.yaml -n ${Namespace}"
        }
    } catch (err) {
        currentBuild.result = 'FAILURE'
        throw err
    }
}
