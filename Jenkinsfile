node {
    def app
    stage('Clone repository') {
        git 'https://github.com/s0obang/opensource_ci.git'
    }
    stage('Build image') {
        app = docker.build("s0obang/opensource_ci_test")
    }
    stage('Test image') {
        app.inside {
            sh 'make test'
        }
    }
    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 's0obang') {
           app.push("${env.BUILD_NUMBER}")
           app.push("latest")
        }
    }
}
