pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo '----------------------------------------------------------'
                echo '                         Building'
                echo '----------------------------------------------------------'
                
                mvn clean package docker:build
            }
        }
    }
}