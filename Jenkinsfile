pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo '----------------------------------------------------------'
                echo '                         Building'
                echo '----------------------------------------------------------'
                
                sh 'pwd'
                sh 'mvn clean package docker:build'
            }
        }
    }
    post {
        always {
            echo 'Build completed'
        }
        success {
            echo 'Successfully!'
        }
        failure {
            echo 'Failed!'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
    options {
        timeout(time: 60, unit: 'MINUTES')
    }
}