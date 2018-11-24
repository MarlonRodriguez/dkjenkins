node {
    def app
    stage('Build Docker Image') {
        checkout scm
        app = docker.build('marlonrod/sample-app:latest')
    }
    
    stage('Publish to Docker Hub') {
        docker.withRegistry("https://index.docker.io/v1/", "dockerhub"){
            app.push('latest')
        }
    }

    stage('Deploy to Production'){
        docker.withServer('tcp://192.168.56.102:2376', 'development') {
            sh 'docker run -d marlonrod/sample-app'
        }
    }
}
