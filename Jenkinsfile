node {
    def app
    stage('Build Docker Image') {
        sh 'echo "192.168.56.102     centus02" >> /etc/hosts'
        checkout scm
        app = docker.build('marlonrod/sample-app:latest')
    }
    
    stage('Publish to Docker Hub') {
        docker.withRegistry("https://index.docker.io/v1/", "dockerhub"){
            app.push('latest')
        }
    }

    stage('Deploy to Production'){

        docker.withServer('tcp://centus02:2376', 'production') {
            sh 'docker run -d marlonrod/sample-app'
        }
    }
}
