pipeline {
    agent none
    stages('Build backend') {
        node {
        checkout scm
        def testImage = docker.build("test-image", "./dockerfiles/test") 

    testImage.inside {
        sh 'make test'
    }
}
    }
}