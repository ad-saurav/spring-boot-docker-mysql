pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    environment {
        DOCKER_HOME = tool('mydocker')
        PATH = "${DOCKER_HOME}/bin:$PATH"
    }
    stages {
        stage('Build') {
            steps {
                echo '----------------------------------------------------------'
                echo '                        Building Jar                      '
                echo '----------------------------------------------------------'
                
                sh 'pwd'
                sh 'mvn clean package'
            }
        }
        stage('Build Image') {
            steps {
                echo '----------------------------------------------------------'
                echo '                      Building Image                      '
                echo '----------------------------------------------------------'
                
                // echo $DOCKER_HOME
                sh 'echo $PATH'
                
                script {
                    app = docker.build("saurav/spring-boot-docker-mysql")
                }
            }
        }
        stage('Push Image') {
            steps {
                echo '----------------------------------------------------------'
                echo '                      Pushing Image                       '
                echo '----------------------------------------------------------'
                
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        app.push("${BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Build completed'
            
            // Clean up our workspace.
            deleteDir()
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