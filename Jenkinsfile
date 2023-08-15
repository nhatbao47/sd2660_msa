pipeline {
    agent none
    stages('Build backend') {
        build() {
            node {
    checkout scm
    def testImage = docker.build("test-image", "./src/backend")

    testImage.inside {
        sh 'make test'
    }
}
        }
    }
}